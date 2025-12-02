# reach-documentation

The Reach documentation package is generated (deployed) on github by merging a pull request. Pull requests are created by a github workflow script that runs when changes to the C stack are comitted. You should consider the reach-c-stack to contain the actual sources of the documentation.

The c-stack workflow requires a Personal Access Token (PAT). These expire, so you may need to create a new one. You can do it from you github account. Some hints are below.

When you intend to make changes to the docs, first run doxygen and sphinx locally. See the workflow script in reach-c-stack for details of the calls.

When the workflow completes it will have created a pull request onto this repository. This must be accepted and published to main, as it is the main branch that is displayed publically.



### What token you need

Use a **classic Personal Access Token (PAT v1)** for the PR-creation step.

**Classic PAT required scopes:**

- `repo` ✅ (to read/write contents and push branches)

- `pull_requests` isn’t a separate classic scope; it’s covered by `repo`

- If your org uses SAML/SSO, you must **authorize the token for the org** after creating it. [The GitHub Blog+1](https://github.blog/2022-10-18-introducing-fine-grained-personal-access-tokens-for-github/?utm_source=chatgpt.com)

### What to do

1. Create a **classic** PAT:  
   GitHub → Settings → Developer settings → Personal access tokens → **Tokens (classic)** → Generate new token

2. Scopes: check **`repo`**.

3. Copy the token.

4. Replace the secret value `REACH_DOCUMENTATION_PAT` with this new classic PAT.

Your existing workflow (push + `gh pr create` with `GH_TOKEN: ${{ secrets.REACH_DOCUMENTATION_PAT }}`) should then work.

The docs generate workflow can also be run manually from the actions tab in the C stack repo.
