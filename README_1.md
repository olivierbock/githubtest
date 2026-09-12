# GRUAN RS41 + ERA5 processing: reviewed structure and proposed refactor

This package contains a proposed refactor of the supplied MATLAB orchestration code. It does not contain or change `compute_ztd_rs41_aparicio2026.m`. Install the `matlab/` overlay into your existing GRUAN repository, which supplies that kernel, common readers, metadata and external dependencies. `reference_original/` preserves all eleven uploaded files byte for byte; do not add that directory to the MATLAB path.

Validation here: all twelve new/modified MATLAB files parsed without syntax errors using the tree-sitter MATLAB grammar. MATLAB, the scientific kernel, `read_nc_file`, metadata CSVs and actual RS/ERA5 data were not available, so execution, `parfor` classification and numerical equivalence have NOT been verified. Run the MATLAB checks below before replacing an operational workflow.

## 1. Project structure

The existing separation into `common`, `products`, `analyses`, `workflows`, `tests` and `dev` is appropriate. Keep that structure. The distinction is responsibility, not whether a filename begins with `run_`.

| Location | Responsibility and examples |
|---|---|
| `docs/` | Data acquisition instructions, file schemas, units, coordinate/time conventions, processing methods, reproducibility instructions |
| `metadata/` | Small curated station association tables, source documentation, controlled metadata releases |
| `matlab/common/` | Reused readers, time/coordinate helpers, common station association logic |
| `matlab/products/rs_metadata/` | Download/extraction modules and machine-readable inventory products |
| `matlab/products/compute_ztd_rs41_era5/` | One-year batch function, unchanged profile kernel, export function |
| `matlab/workflows/` | Multi-system/year compute and export schedulers; eventually end-to-end orchestration |
| `matlab/analyses/<analysis>/` | RS characteristics, intercomparison, scientific diagnostics and publication plots |
| `matlab/config/` | Tracked scientific experiments and environment example; ignored machine-local environment |
| `matlab/tests/` | Small orchestration tests, regression comparisons and existing scientific tests |
| `matlab/dev/` | Exploratory code; excluded from automatic path setup |
| Outside Git repository | Raw NetCDF/ERA5/GNSS data and generated result folders |

The two physical-decomposition plotting scripts could eventually move from the product module to an analysis folder. They are not moved or rewritten in this overlay: retaining their current location avoids mixing a plotting migration into the computing refactor. Similarly, reconcile `updated_compute_rs_summary_statistics_and_plots.m` with its unprefixed counterpart rather than retaining competing production implementations indefinitely.

The supplied setup adds `GRUAN/matlab/utils`, whereas `content.txt` lists shared readers under `matlab/common` and does not list `utils`. This is a discrepancy to check in the real checkout, not proof that the directory is absent. `gruan_startup` uses the documented `common` location and explicit code folders.

## 2. Answers to the proposed changes

| Question | Recommendation |
|---|---|
| Move both run schedulers into `workflows`? | Yes. The revised schedulers are functions there, with explicit inputs. |
| Add `run_compute_ztd_batch_rs41_era5.m` under `analyses`? | No need. Product generation remains in `products`; call the batch function directly or select one job through the workflow. An optional personal launcher belongs in ignored `matlab/local`, or a reproducible launcher in `workflows`. |
| Turn the batch script into a function? | Yes: `result = compute_ztd_batch_rs41_era5(cfg, opts)`. It returns status/counts/output paths without retaining the large output arrays in the caller. |
| Is requiring both setup and config acceptable? | The separation of concerns is good; reliance on scripts injecting variables into one workspace is fragile. Replace setup with an environment function and scientific config with a function returning structures. |
| Global and local configuration? | Use project-wide defaults plus machine-local paths, not MATLAB `global` variables. Explicit scientific overrides belong in tracked experiment functions. |
| One launcher for every analysis? | Only where it simplifies a meaningful public interface. A reusable analysis function accepting input paths/settings is often sufficient. Small exploratory scripts do not need wrappers. |
| Trace different `cfg`/`opts`? | Track experiment definitions in Git, and store resolved settings and provenance with each separately named result run. Git does not replace a result catalogue. |

MATLAB functions have separate workspaces, making the scheduler/batch boundary explicit. In particular, function-scoped `onCleanup` runs when the function exits; the uploaded script's cleanup object can survive in the shared workspace. See [MathWorks cleanup documentation](https://www.mathworks.com/help/matlab/matlab_prog/cleaning-up-when-the-function-completes.html).

The annual `parfor` structure is preserved: the outer scheduler is serial over product/system/year, and the batch distributes NetCDF files among workers. No nested parallelism is introduced. Retain the existing sliced cell arrays for worker results. See [MathWorks parfor documentation](https://www.mathworks.com/help/parallel-computing/parfor.html).

## 3. Configuration responsibilities and precedence

1. `gruan_startup()` adds explicit project code paths. It does not start computing, load scientific settings, clear variables, close figures or start a pool.
2. `gruan_environment_local(repoRoot)` returns absolute machine paths. Copy and rename the example once on each computer. Keep this local file out of Git. The Windows/Linux examples include placeholders requiring your actual Linux paths.
3. `config_ztd_batch_rs41_era5()` returns the scientific defaults supplied in the attachment, with the explicitly documented changes below.
4. A tracked experiment function loads those defaults and applies explicit scientific overrides. It also defines selected systems/years and execution settings.
5. The scheduler constructs fresh `jobCfg` values, overriding job paths, metadata snapshot paths, product/system/year and operational settings. It does not mutate the original `cfg` or `opts`.
6. Within each sounding/GNSS computation, the existing `optsThis.z0_m` and `optsThis.groundCheck` overrides remain unchanged.

No automatic deep merges or hidden machine-specific scientific overrides are introduced. If different stations need different physics/quality settings, use separate named experiments initially. A future per-system override mechanism should save the fully resolved options for each job, not rely on caller workspace state.

## 4. Installation and first execution

1. Create a local Git branch in your real checkout, for example `git switch -c refactor/ztd-workflow`.
2. Copy the package's `matlab/` files to the matching repository paths. Keep your existing kernel and common functions.
3. Remove the old `run_ztd_scheduler_rs41_era5.m` and `run_export_ztd_summary_scheduler.m` from the product directory after installing their replacements under `workflows`. Use `git rm` to record these removals. Leaving duplicate function names on the path is unsafe.
4. Retire the old module `setup.m`/`setup_example.m` after transferring any private settings. Original copies remain in this package for reference. Do not apply this change to unrelated analysis setup scripts.
5. Append `gitignore_additions.txt` to your existing `.gitignore`.
6. Copy `gruan_environment_example.m` to `gruan_environment_local.m`, rename its first-line function, and set the correct absolute paths. Add any required external toolbox paths in your own startup.
7. From the repository root:

```matlab
addpath(fullfile(pwd, 'matlab'));
repoRoot = gruan_startup();
env = gruan_environment_local(repoRoot);
[selection, execution, cfg, opts] = ztd_experiment_example();
which compute_ztd_rs41_aparicio2026 -all
which compute_ztd_batch_rs41_era5 -all
which run_ztd_scheduler_rs41_era5 -all
report = run_ztd_scheduler_rs41_era5(env, selection, execution, cfg, opts);
```

The example selects ten LAU-RS-02 files from 2021 in serial mode. If that subset is unavailable, select one that exists. The scheduler remains year-based; `maxFiles` is only a controlled smoke-test subset, not a different production partitioning scheme.

After validating the sample, set `execution.maxFiles = Inf`, enable `execution.useParallel`, expand the selection and choose a NEW `execution.runId`. Use the same committed experiment on Linux, with the Linux local environment function. A small tracked wrapper can run these lines under `matlab -batch`; it need not exist for every module.

For one job you can also call the batch directly after setting `cfg.rsDir`, `cfg.era5Dir`, `cfg.outDir`, `cfg.system`, and the two metadata filenames. Its output folder must be empty. The direct call writes resolved job inputs and outputs, but run-level Git/source/metadata snapshots are supplied by the scheduler. Selecting one system/year through the scheduler is therefore the preferred traceable entry point.

## 5. Results and provenance

Each run has a unique human-readable `execution.runId`, for example `aparicio2026_baseline_20260912_01` or `aparicio2026_dp25_20260912_01`. It is an identifier, not a calculated configuration hash. The scheduler refuses an existing run directory; the batch refuses a nonempty job directory.

| Relative path under `<resultsRoot>/<runId>/` | Content |
|---|---|
| `run_config.mat` | Requested cfg/opts, execution/selection, environment, job list, start UTC, Git state, MATLAB/platform/toolbox versions |
| `metadata/gnss_rs_association.csv` | Exact copied association table used by every job |
| `metadata/gnss_info.csv` | Exact copied GNSS station table used by every job |
| `code_snapshot/` | Selected source files resolved by MATLAB `which`, including the existing scientific kernel when available |
| `job_status.csv` | Pending/running/completed/completed_with_errors/failed/skipped jobs, counts and error reports |
| `<product>/<system>/<year>/job_inputs.mat` | Resolved cfg/opts, selected RS file inventory, year-directory ERA5 inventory and GNSS station table |
| `<product>/<system>/<year>/ztd_summary.csv` | All sounding/station attempt rows, including failures |
| `<product>/<system>/<year>/ztd_results_all.mat` | Existing result variables plus `allOutSummaryRow`, an explicit mapping into the summary |
| `<product>/<system>/<year>/ztd_batch_log.txt` | Batch messages |
| `<product>/<system>/<year>/per_profile/` | Optional individual result files, as in the original code |
| `run_finished.mat` | Finish UTC and final job report; its presence does not imply all jobs succeeded |

A job without associated GNSS stations is now a failed job instead of writing an empty summary only. A run may finish with skipped or failed jobs: inspect `job_status.csv`. If MATLAB is killed, a job may remain `running` and there may be no finish record. That is an incomplete run, not a successful cached result.

There is no automatic resume in this first refactor. Re-run failed selections under a new run ID; retain the failed run for diagnosis. Do not write to or synchronize the same active run directory from two computers. The fresh-folder checks are protection against ordinary accidental overwrites, not a distributed locking protocol. Publish/sync completed run directories with a single writer.

The recorded RS inventory has filenames, byte counts and timestamps for the exact selected files. The ERA5 inventory is a SUPerset: all `*.mat` files in the relevant year directory. It does not prove which bytes were read, and timestamps/sizes are not content hashes. Input mutation during processing is not detected. For publication-grade reproducibility, freeze raw input releases and build a SHA-256 inventory once during acquisition; reference that immutable release/checksum catalogue from the experiment. Do not repeatedly hash large annual files inside `parfor`.

Git records the commit, worktree status and diff against HEAD. Selected source files are copied, but transitive external dependencies and untracked files are not exhaustively archived. A custom `opts.eosFcn` may reference code outside this snapshot. For production releases, commit the code first, pin external dependencies and retain their versions/source archives. A dirty working tree is recorded, not prohibited.

For tracking many runs, maintain a small experiment catalogue with run ID, scientific question, parent/baseline run ID, changed settings, input release ID, Git commit, path, completion/QC status and notes. The catalogue can be versioned in Git if small. Keep bulk numerical products outside Git. Canonical config hashes can be added later; MATLAB structures/function handles need deliberate canonical serialization, so a casual `jsonencode` hash is not included here.

## 6. Independent export

After computation:

```matlab
runDir = fullfile(env.resultsRoot, execution.runId);
run_export_ztd_summary_scheduler(runDir, selection.products, ...
    selection.systems, selection.years);
```

The exporter reads that run's summaries, not the original RS/ERA5 inputs. It uses no compute setup/config. Numeric CSV formatting now defaults to `[]` to avoid the previous `%.3f` string rounding. The source MAT remains the numerical reference; CSV is for exchange.

Exports are written under `ztd_summary_export/<product>/`, preventing collisions between RS product versions with the same system/year/station IDs. The existing pair filename and manifest schema are preserved within each product folder. Export settings are saved in `export_config.mat`.

Export filtering retains the supplied default `requireStatusOk=true`, `requireUsable=false`. For a scientific intercomparison you will often want usable rows only, but that decision must be explicit:

```matlab
exportSettings = struct('exportName', 'ztd_summary_export_usable', ...
    'requireUsable', true, 'numericFormat', []);
run_export_ztd_summary_scheduler(runDir, selection.products, ...
    selection.systems, selection.years, exportSettings);
```

The export scheduler requires a fresh named export directory. This prevents stale CSVs surviving when a later filtering choice removes an entire pair. A failed export can leave partial files; use its console errors and pair manifests to assess completeness, then retry under a new export name. Direct calls to the low-level export function retain its original overwrite behaviour; use the scheduler for separated export variants.

RI41 ground-check extraction is intentionally not coupled into the new compute scheduler. The uploaded `export_rs41_groundcheck_ri41.m` defines `groundCheckInputMode` but always scans/reads NetCDF; the `existing_csv` option selected in setup is not implemented there. Its correction belongs in the metadata workflow. The kernel's existing per-sounding `groundCheck` input is still passed by the batch.

## 7. Specific code findings and changes

| Finding in supplied code | Treatment |
|---|---|
| Batch/export scripts share scheduler workspace | Converted to functions with explicit cfg/opts inputs; export no longer changes the scheduler cfg |
| `setup.m` depends on caller variable `schedulerDir` | Replaced by independent environment/config/experiment functions |
| `perFileDir` dereferenced without default | Default is now empty, disabling individual saves |
| Baseline configuration reloaded in every job | Load once; construct a fresh jobCfg per job |
| T/Z nearest timestamps have no tolerance; condensate may use another hour | Require timestamps within `cfg.maxEra5FieldTimeDiff_seconds` of humidity; new default 1 second. RS-to-humidity tolerance remains 2 hours |
| Invalid/empty ERA5 time axes can escape meaningful checks | Reject empty/nonfinite axes |
| Success summary row appended before retained output is built | Prepare row/output/log message before appending the successful pair; keep existing success-only `allOut` semantics |
| No explicit output-to-summary mapping | Save and assert `allOutSummaryRow` |
| Missing condensate flags lost when individual files disabled | Add availability and relative-time columns to summary |
| Outer scheduler aborts on a job error | Record job-level errors and continue unless `stopOnJobError=true` |
| Serial mode still reaches `gcp` at scheduler end | Pool operations only when requested; cleanup only deletes a pool owned by this scheduler |
| Repeated filenames overwrite results | Separate fresh run/job directories |
| Pair export can collide across product versions | Product-specific export directory |
| Three-decimal export rounding | Default to numeric CSV output; explicit format remains available |
| `cfg.missingEra5Mode='skip'` is never consumed | Remove misleading setting; missing required files produce error rows, with `cfg.stopOnError` controlling aborts |
| `scheduler.savePerFileResuls` typo | Replace with `execution.savePerFileResults` |

The stricter ERA5 timestamp check is a deliberate batch input-validation change. Previously mismatched fields may now produce error rows. The kernel, humidity-hour nearest-neighbour choice, horizontal interpolation, profile preparation, integration and scientific defaults otherwise remain as supplied. Do not claim identical results on previously invalid input sets.

## 8. Scientific/data issues to investigate separately

These are review findings, not fixes silently folded into the kernel:

- `bilinearProfile` clamps weights to the grid boundary, falls back to nearest on a non-2x2 coordinate set, and does not unwrap longitude around the dateline. Those behaviours can hide poor spatial collocation. Record grid geometry, station-to-RS distance and interpolation mode/fallback before interpreting outliers.
- GNSS metadata selects the first matching station row. Epoch-dependent coordinates/antenna changes need explicit validity intervals, and aliases such as `alt` do not establish the vertical datum. Confirm antenna reference point, orthometric/geometric/geopotential conventions and units.
- `getRadiosondeTime` takes the first usable time or a filename-derived time; numeric candidates are assumed to be MATLAB datenums. Verify launch versus measurement-time semantics and UTC handling for the actual reader. The batch reduces the time field to one reference time; assess whether time-resolved drift collocation is required before changing this.
- Humidity is matched to the nearest ERA5 hour within 2 hours. No time interpolation or adjacent-year search is implemented. Quantify actual offsets and year-boundary gaps.
- Annual ERA5 MAT files are loaded again inside each sounding/station operation. This can dominate I/O. Benchmark before introducing worker-local caches or `parallel.pool.Constant`: replicating annual arrays across workers can exhaust memory. Keep a process pool initially until thread compatibility of the reader and kernel is verified.
- The defaults retain only `out.section6` in `allOut`. Confirm that it contains the diagnostics required by every downstream plot. The two plotting scripts expect different input layouts and some top-level fields/flags. For validation, set `cfg.keepSection6OnlyInAllFile=false`, `cfg.keepFullOutputsInAllFile=true`, and enable individual files for a small subset.
- An RS-triggered ERA5-only calculation is sampled at the sounding times and associated GNSS locations. It is not a continuous hourly ERA5-only GNSS product. If needed, add a separate station/time-grid producer later using the same documented physics.
- Intercomparison needs one common sampling/quality policy across RS+ERA5, ERA5-only and each GNSS provider. Preserve rejected matches and exclusion reasons so different coverage does not masquerade as a physical bias.

## 9. Acquisition and downstream roadmap

For each GRUAN launch/station CSV, NetCDF data release, derived metadata table, ERA5 extraction and GNSS provider product, document: source endpoint, retrieval UTC, release/version, original filename, checksum, units, reference frame and vertical datum, time convention, station aliases and license/citation. Keep downloaded source metadata separate from manually curated association decisions.

Represent association explicitly: GRUAN site, RS system, GRUAN GNSS alias (e.g. BAR-GN-01), physical GNSS ID (e.g. UTQI), provider-specific ID, validity dates and association rationale. Do not assume the alias is itself the provider's station code.

Add provider adapters for GFZ MAT, NGL MAT and SPOTGINS ZTD inputs when their schemas are available. Normalize to a documented table containing station ID, epoch UTC, ZTD in one unit, uncertainty/quality flags, provider/solution/version, reference point, source file and processing status. The supplied files do not establish these provider schemas, so no speculative readers are included.

Intercomparison should consume explicit run IDs and provider releases. Each analysis result should save its parent product run IDs, filters, collocation tolerances, sampling counts and analysis code/config version. Publication figures can then be regenerated independently of the expensive product computations.

## 10. MATLAB validation before an operational run

```matlab
checkcode(which('compute_ztd_batch_rs41_era5'));
checkcode(which('run_ztd_scheduler_rs41_era5'));
r = runtests(fullfile(repoRoot,'matlab','tests','test_ztd_workflow.m'));
assert(all([r.Passed]));
```

The supplied tests cover per-system year discovery, duplicate selection removal and overwrite protection. They are supplied for execution in MATLAB and were not run here.

Then use exactly the same input subset and scientific options with the old and new batches in separate output folders, on ERA5 files sharing a common time axis. Run:

```matlab
addpath(fullfile(repoRoot, 'matlab', 'tests'));
assert_ztd_regression(referenceMat, candidateMat);
```

This helper compares common numeric summary columns, flags, times and attempt keys, and verifies the explicit output mapping. It does not compare every nested scientific output or replace the existing kernel tests. Its absolute tolerance is in each column's native units and defaults to 1e-10; adjust only with a justified numerical criterion.

Repeat the small revised case in serial and parallel modes, compare summaries, and inspect logs. Exercise a missing mandatory ERA5 file, a mismatched T timestamp and a missing `section6` output in a controlled fixture: each must become an error without a spurious success row. A no-association job must be marked failed. Verify that a second job still runs when the first fails and `stopOnJobError=false`. These integration cases require the real reader/kernel or appropriate test fixtures and have not been executed here.

Only then process a complete system/year and check counts, usable fractions, ERA5 timing offsets and scientific residuals before expanding to all systems/years. Commit the validated changes and experiment definition, push to GitHub, and pull the same commit on Linux. This package has not modified your PC checkout or pushed to GitHub.
