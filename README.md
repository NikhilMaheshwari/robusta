# Installing Robusta as a user
If you want to use Robusta, see our [installation guide](https://robusta.dev/docs/getting-started/installing.html).

# Installing Robusta runner in cluster as a developer
If you want to develop features for Robusta itself you'll need to install Robusta from source:

1. `git clone` the source code. 
2. Install skaffold and kustomize.
3. Run `skaffold run --tail`

If you want to use the Slack integration:
1. Get a slack token from https://robusta.dev/integrations/slack/?id=xyz
2. Create your private `active_playbooks.yaml` file. 
You can use `robusta gen-config` to do that.
3. Move the generated file `active_playbooks_generated.yaml` to the `deployment` directory before running skaffold
4. Optional: reduce the chance you'll accidentally commit your Slack key to git by running `git update-index --skip-worktree helm/robusta/active_playbooks.yaml` (see [here](https://stackoverflow.com/a/40272289/495995) for details)

# Running Robusta runner locally as a developer
If you want to run the Robusta runner on your own computer (e.g. with telepresence):

1. `git clone` the source code
2. `cd src`
3. `poetry install`
4. `poetry run python3 -m robusta.runner.main`

If you're on Mac OS and receive errors about `Pillow` or `libjpeg` when running `poetry install` then run `brew install libjpeg` first.

# Running Robusta cli locally as a developer
This is only necessary if you are developing features for the cli itself.
If you just want to develop robusta-runner and install it from your local version,
use the skaffold instructions above. 

### Using poetry

1. `git clone` the source code
2. `cd src`
3. `poetry install`
4. `poetry run robusta`

### Alternative method using pip
This method installs robusta into your global python environment

1. `git clone` the source code
2. `cd src`
3. `pip3 install .`

# Running Tests
1. Set a Slack token in `tests/config.env`
2. `cd src && python -m pytest ..` (add `-s` to print all pytest output and `--keep-cluster` to keep the test KIND cluster alive after tests finish) 
3. Optional: reduce the chance you'll accidentally commit your Slack key to git by running `git update-index --skip-worktree tests/config.env`