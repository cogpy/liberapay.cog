> ## Engineering Solution Masterpiece: Resolving failing job in GitHub Actions (Job ID: 56133659637)
> 
> ### Problem Summary:
> 
> The job failed due to two critical issues:
> 
> 1. Git LFS smudge filter failed to download LFS-tracked files (notably www/assets/fonts/ubuntu-bold-italic-webfont.ttf) due to authentication or missing setup.
> 2. 'git checkout' aborted due to untracked working tree files which would be overwritten, indicating the need for cleaning state before branch transitions.
> 
> ### Solution Implemented:
> 
> - Added steps in the workflow for installing and initializing Git LFS, ensuring all required large files (fonts, media) are pulled and accessible.
> - Included explicit `git lfs pull` immediately after cloning.
> - Integrated a `git clean -fdx` step before any branch checkout to remove untracked files that cause abort errors.
> - Provided fallback logic for missing branches (checkout main if the desired feature branch does not exist).
> 
> ### Workflow improvements (YAML):
> 
> steps:
>   - name: Install Git LFS
>     run: sudo apt-get update && sudo apt-get install -y git-lfs
>   - name: Initialize LFS
>     run: git lfs install
>   - name: Clone repository
>     run: git clone --branch ${{ github.ref\_name }} https://github.com/cogpy/liberapay.cog.git
>   - name: Pull all LFS blobs
>     working-directory: liberapay.cog
>     run: git lfs pull
>   - name: Clean working tree
>     working-directory: liberapay.cog
>     run: git clean -fdx
>   - name: Checkout target branch
>     working-directory: liberapay.cog
>     run: git checkout copilot/optimize-performance || git checkout main
> 
> ### Issue to be opened for QA:
> 
> - Install and ensure Git LFS setup.
> - Clean up workspace before branch transitions.
> - Add error handling for missing branches.
> - Test full workflow by triggering the failing job and reviewing logs for successful LFS fetch and branch transitions.
> 
> Refer to the attached \[job logs (ref: [b7d918e](https://github.com/cogpy/liberapay.cog/commit/b7d918ecd2f8fd55eb96fa558b763e9f4b6c630d))\] and ensure all associated changes resolve both Git LFS and checkout errors.

*This pull request was created as a result of the following prompt from Copilot chat.*

> ## Engineering Solution Masterpiece: Resolving failing job in GitHub Actions (Job ID: 56133659637)
> 
> ### Problem Summary:
> 
> The job failed due to two critical issues:
> 
> 1. Git LFS smudge filter failed to download LFS-tracked files (notably www/assets/fonts/ubuntu-bold-italic-webfont.ttf) due to authentication or missing setup.
> 2. 'git checkout' aborted due to untracked working tree files which would be overwritten, indicating the need for cleaning state before branch transitions.
> 
> ### Solution Implemented:
> 
> - Added steps in the workflow for installing and initializing Git LFS, ensuring all required large files (fonts, media) are pulled and accessible.
> - Included explicit `git lfs pull` immediately after cloning.
> - Integrated a `git clean -fdx` step before any branch checkout to remove untracked files that cause abort errors.
> - Provided fallback logic for missing branches (checkout main if the desired feature branch does not exist).
> 
> ### Workflow improvements (YAML):
> 
> steps:
>   - name: Install Git LFS
>     run: sudo apt-get update && sudo apt-get install -y git-lfs
>   - name: Initialize LFS
>     run: git lfs install
>   - name: Clone repository
>     run: git clone --branch ${{ github.ref\_name }} https://github.com/cogpy/liberapay.cog.git
>   - name: Pull all LFS blobs
>     working-directory: liberapay.cog
>     run: git lfs pull
>   - name: Clean working tree
>     working-directory: liberapay.cog
>     run: git clean -fdx
>   - name: Checkout target branch
>     working-directory: liberapay.cog
>     run: git checkout copilot/optimize-performance || git checkout main
> 
> ### Issue to be opened for QA:
> 
> - Install and ensure Git LFS setup.
> - Clean up workspace before branch transitions.
> - Add error handling for missing branches.
> - Test full workflow by triggering the failing job and reviewing logs for successful LFS fetch and branch transitions.
> 
> Refer to the attached \[job logs (ref: [b7d918e](https://github.com/cogpy/liberapay.cog/commit/b7d918ecd2f8fd55eb96fa558b763e9f4b6c630d))\] and ensure all associated changes resolve both Git LFS and checkout errors.
