# git flow - workflows
The actions in this repo are setup to match a basic git flow as follows:
```mermaid
flowchart TB


A-->H-->A
D-->F-->D
D-->B-->D
D-->R
R-->A-->D

D("develop")
R("release v1.1.0")
F("feature")
B("bugfix")
A("main v1.0.0")
H("hotfix v1.0.1")



```
1. The `main` branch houses and matches the latest release and PRODUCTION code.
2. Hotfixes are created from the `main` branch and merged back into the `main` branch.
3. Updates to the `main` branch are synced into `develop`.
4. `feature/` & `bugfix/` branch from `develop` and are merged back into `develop`
5. Releases are made from the `develop` branch, and upon passing QA are merged into `main`
6. Updates to the `main` branch are tagged, released, published, and deployed.
7. All version bumping is done automatically by the actions, aka ๐ค workflow[bot]
8. PR's are automatically created when pushing branches with a prefix of `feature/` or `bugfix/`
9. There are two dispatchable workflows that can be used to initiate a `hotfix/` or `release/`
10. When using the two workflows above, they too will create PR's to be merged into `main` 

### The workflows:
- ๐ค๐ฃ Announce Release
	- Creates a release from the tag matching the version found in package.json 
- ๐ค๐ญ Build
	- Runs `npm ci` , `npm run test` , and `npm run build`
- ๐ Changelog CI
	- Generates a changelog
- ๐ค๐ Deploy Production ๐ฌ
	- Deploy to production
- ๐ค๐ Deploy Staging ๐งช
	- Deploy to staging
- ๐๐ Dispatch hotfix branch
	- Dispatch `hotfix/` branch and auto bump `patch` number
- ๐๐ Dispatch next minor release
	- Dispatch `release/` branch and auto bump `minor` number
- ๐๐ Dispatch next major release
	- Dispatch `release/` branch and auto bump `major` number
- ๐ค๐ [PR] bugfix > develop
	- Automatically create PR to `develop` branch when pushing `bugfix/` branch
- ๐คโจ [PR] feature > develop
	- Automatically create PR to `develop` branch when pushing `feature/` branch
- ๐ค๐ฆ Publish Release
	- Runs `npm ci`, `npm run build`, and `npm publish`
- ๐คโฉ Synchronize develop
	- Keeps `develop` branch in-sync with all updates to `main`
- ๐ค๐ Tag main
	- Tag Repo using `version` found in `package.json`
	- Announce Release from same tag
	- Sync Dev - Deploy to stagin
	- Deploy to Prod

