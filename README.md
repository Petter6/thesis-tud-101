# DAIC Cluster & Thesis Survival Guide

## 1. Storage

### Writable Locations

- **Home folder (`~/`)**
  - Small quota
  - Available on every node
  - Good for configs, scripts, small files
- **`/tmp` folder**
  - Node-local (different for every node)
  - Good for temporary installs 

### Large Storage: Studentscvlab

- Request access from **Marunka**
- Path: `/tudelft.net/staff-umbrella/StudentsCVlab/`
- ⚠️ Windows-based → **cannot install Conda/envs here**

---

## 2. Apptainer (Recommended)

Because you cannot install envs directly in Studentscvlab, use a
container.

### Why Apptainer?

- More stable than installing conda in `/tmp` and moving dirs around
- Avoids repeated re-installs if you need new dependencies
- Reproducible and portable
- Worth the initial setup

### GPU Usage

Use `--nv` to enable CUDA:

```bash
apptainer exec --nv container.sif python your_script.py
```

### Workflow

- Build container once (on local machine or cluster)
- Store `.sif` in Studentscvlab
- Use home directory for configs & job scripts

---

## 3. Modules

List available modules:

```bash
module avail
```

Load CUDA:

```bash
module load cuda/<version>
```

Fix GLIBC / compiler errors:

```bash
module load devtoolset/<version>
```

---

## 4. Jobs & Sessions

### Interactive Sessions (Debugging)

- Typically 1 hour max
- Good for:
  - Debugging 
  - Running small scripts
  - Testing SLURM setup

### Batch Jobs (Long Runs)

Submit with:

```bash
sbatch job.sbatch
```

#### QOS (Priority Levels)

- `low`
- `medium`
- `high`
- `infinite`

Priority depends **only on QOS**, not the time you request. Time only
controls when your job gets **killed** if it runs too long.

### Job Arrays

Use arrays to run many jobs at once:

```bash
#SBATCH --array=0-9
```

Great for: - Hyperparameter sweeps - Multiple configs - Dataset variants

### Partitions

Use one of: - `--partition=prb,insy,general`

❗ If you don't specify these, you can only use the general gpus. 

---

## 5. Syncing Local ↔ Cluster Code

Use **Unison** (recommended) to keep local and cluster code in sync.

Benefits: - No manual `rsync` - Fast incremental sync - Works both
directions

---

## 6. Useful Extensions

### Google Scholar PDF Reader

- Lets you jump straight to references
- Gives BibTeX faster
- Reduces scrolling time significantly

---

## 7. REIT / DAIC Courses

Highly recommended (\~4 hours in the morning):, Cluster usage, Python reproducibility, Apptainer tips & tricks etc. 

These save a lot of time in the long run.

---

## 8. Thesis Writing Guidelines

### Key Principles

- Always explain **why** you do something:
  - Why this graph?
  - Why this experiment?
  - Why this related work?
  - Why this dataset or metric?
- Make **every reasoning step explicit**
- Research writing is not about being fancy; it's about clarity and
  logic
- Follow the writing guidelines: https://jvgemert.github.io/writing.pdf

### Figures & Tables

For every figure: 1. What question does it answer? 2. What should the
reader conclude? 3. How does it fit into the storyline?

### Storyline Format

Follow the structure strictly: https://jvgemert.github.io/storyline.pdf

### Final Step

- **Run a spell check** before sending anything called "final"

---

## 9. Thesis Deadlines & Administration

Deadlines are strict!

### Greenlight → Defense

There must be **6 weeks** between: - Greenlight meeting - Actual defense

To finish in the same calendar year → schedule greenlight **early June
at the latest**.

### Final Thesis Submission

Send the final thesis to your supervisors **2 weeks before** your
defense.
