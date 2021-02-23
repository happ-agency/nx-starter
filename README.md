# [Nx](https://nx.dev/) starter

> Core setup for the [nx](https://nx.dev/) applications

## Content

1. [Pnpm](#pnpm)
2. [Nx workspace](#nx-workspaces)
3. [Npm check](#npm-check)
4. [Force using pnpm](#force-using-pnpm)
5. [Git](#git)
6. [Git flow](#git-flow)
6. [Husky](#husky)
7. [Commitlint](#commitlint)
7. [Commitizen](#commitizen)
7. [Conventional changelog](#conventional-changelog-cli)
7. [Eslint](#eslint)
7. [Prettier](#prettier)
7. [Stylelint](#stylelint)
7. [Editor config](#editor-config)

## Pnpm
1. Install a [pnpm](https://www.npmjs.com/package/pnpm) globally: `npm i -g pnpm`

	> [pnpm](https://www.npmjs.com/package/pnpm) - package manager, which is much faster then npm and yarn

## Nx Workspaces

1. Create a [nx workspace](https://nx.dev/): `pnpx create-nx-workspace WORKSPACE_NAME --preset=empty --no-nxCloud --package-manager=pnpm --defaultBase=main`

	> [pnpx](https://pnpm.js.org/en/pnpx-cli) - pnpm package runner
	
	> 1. `WORKSPACE_NAME` - name of workspace
	> 2. `--preset=empty` - preset to use
	> 3. `--nxCloud` - use nx cloud or not
	> 4. `--package-manager=pnpm` - default package manager
	> 5. `--defaultBase=main` - default git branch

## Npm check
1. Install a [npm-check](https://www.npmjs.com/package/npm-check) only for development: `pnpm i -D npm-check`

	> [npm-check](https://www.npmjs.com/package/npm-check) - package that check for outdated, incorrect, and unused dependencies.

2. Update `package.json` with:

	 <details>
	 	<summary>package.json</summary>

		{
			...
				"scripts": {
					...
				 	"check-packages": "npm-check",
				 	"update-packages": "npm-check -y"
				}
			...
		}
	 </details>

## Force using pnpm

1. Create `.npmrc` in the root folder with:
	 
	<details>
		<summary>.npmrc</summary>

		engine-strict = true
	</details>

2. Update `package.json` with:

	 <details>
	 	<summary>package.json</summary>

		{
			...
			"license": "...",
			"engines": {
				 "yarn": "please-use-pnpm",
				 "npm": "please-use-pnpm",
				 "pnmp": ">= 15.4.3"
			},
			"scripts": { ... }
			...	
		}
	 </details>

> Force usign [pnpm](https://www.npmjs.com/package/pnpm) throw `please-use-pnpm` error on [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/) use

## Git

> [Git](https://git-scm.com/)

1. Add origin: `git remote add origin https://github.com/happ-agency/nx-starter.git`
2. Set main branch: `git branch -M main`
3. Push branch: `git push -u origin main`
	
## Git flow

> [Git flow](https://danielkummer.github.io/git-flow-cheatsheet/index.ru_RU.html)
 
1. Create `main` branch: `git branch -M main`
2. Create `develop` branch fron `main`: `git checkout -b develop`
3. Create `feature` branch from `develop`: `git checkout -b feature/xxx`
4. Create `fix` brabch from `develop`: `git checkout -b fix/xxx` 
5. Create `release` brabch from `develop`: `git checkout -b release/xxx`
6. Create `hotfix` brabch from `develop`: `git checkout -b hotfix/xxx` 
	
> 1. We work in the `develop` branch.
> 2. When we start work with the `feature` or `fix`, we create `feature/xxx` or `fix/xxx` from the `develop`.
> 3. After finish the work we create pull request from the `feat/xxx` or `fix/xxx` to the `develop`.
> 4. For the relase create `release/xxx` from the `develop`.
> 5. For the publish create pull request from the `release/xxx` to the `main`.
> 6. After the publish rebase `main` from the `dev` and rebase `dev` from the `feature/xxx` or `fix/xxx`.
> 7. `Hotfix` creates from the `main` and create pull request to the `main` after the finish
> 8. After each changes in the `main` or `develop` we do rebase from connected branches. rebase `main` from `develop`. rebase `develop` from `features` or `fixes`

## Husky

> [Husky](https://www.npmjs.com/package/husky)

1. Install [husky](https://www.npmjs.com/package/husky) only for development: `pnpm i -D husky`
2. Update `package.json` with:
	  <details>
			<summary>package.json</summary>

		 {
			 ...
			 "scripts": { ... },
			 "husky": {
				 "hooks": {
					"pre-commit": "nx lint"
				 }
			 },
			 "private": "...",
			 ...
		 }
	  </details>

## Commitlint

> [Commitlint](https://yarnpkg.com/package/commitlint)

1. Install [commitlint](https://yarnpkg.com/package/commitlint) only for development: `pnpm i -D @commitlint/{config-conventional,cli}`
2. Install [@happ/commitlint-config]() only for development: `pnpm i -D @happ/commitlint-config`
3. Create `.commitlintrc.js` in the root folder with:
	<details>
		<summary>.commitlintrc.js</summary>
		
		module.exports = {
			"extends": ["@happ/commitlint-config"]
		}
	</details>

4. Update `package.json` with:

	<details>
		<summary>package.json</summary>

		 "husky": {
			 "hooks": {
				 ...
				 "pre-commit": "nx lint",
				 "commit-msg": "commitlint -E HUSKY_GIT_PARAMS",
			 }
		 }
	</details>

> Commit have to be like `feat: add auth service`, `fix: remove wrong validation`
>
> You can find all availale types [here](https://github.com/conventional-changelog/commitlint/tree/master/@commitlint/config-conventional)

## Commitizen

> [Commitizen](https://www.npmjs.com/package/commitizen)
> 
> [cz-format-extension](https://www.npmjs.com/package/cz-format-extension) - tool for customize commitizent questions

1. Install [commitizen](https://www.npmjs.com/package/commitizen) only for development: `pnpm i -D commitizen`
2. Install [cz-format-extension](https://www.npmjs.com/package/cz-format-extension) only for development: `pnpm i -D cz-format-extension`
3. Install [@happ/commitizen-config]() config only for development: `pnpm i -D @happ/commitizen-config`
	 > Install it together: `pnpm i -D commitizen cz-format-extension @happ/commitizen-config`
4. Make your repo commitizen-friendly: `commitizen init cz-conventional-changelog --save-dev --save-exact`
5. Create `.czrc` with:

	 <details>
	 	<summary>.czrc</summary>
	 
		 {
			"path": "cz-format-extension"
		 }
	 </details>

6. Create `.czferc.js` with:

	  <details>
	  	<summary>.czferc.js</summary>
	 
		 module.exports = {
			extends: ['@happ/commitizen-config']
		 };
	  </details>

7. Update `package.json` with:

	   <details>
	   	<summary>package.json</summary>
	 
		 {
			...
			"scripts": {
				...
				"git-add": "git add .",
				"git-commit": "cz",
				"git-push": "git push",
				"git": "pnpm run git-add && pnpm run git-commit && pnpm run git-push"
			}
			...
		 }
	   </details>

## Conventional changelog cli

> [Conventional changelog cli](https://www.npmjs.com/package/conventional-changelog-cli)

1. Install [conventional changelog cli](https://www.npmjs.com/package/conventional-changelog-cli) only for development: `pnpm i -D conventional-changelog-cli`
2. Init changelog: `conventional-changelog -p angular -i CHANGELOG.md -s -r 0`
3. Update `package.json` with:

	<details>
			<summary>package.json</summary>
	 
		 {
			...
			"scripts": {
				...
				"changelog": "conventional-changelog -p angular -i CHANGELOG.md -s && git add CHANGELOG.md",
				"version": "pnpm run changelog"
			}
			...
		 }
	</details>

	> Use `pnpm version [major|minor|patch]` to change your project's version and generate changelog
	>
	> `version` script runs automatically on `pnpm version major`

## Eslint

> [Eslint](https://www.npmjs.com/package/eslint)

1. Install [eslint](https://www.npmjs.com/package/eslint) only for development: `pnpm i -D eslint`
2. Install [@happ/eslint-config]() only for development: `pnpm i -D @happ/eslint-config`
3. Install [@happ/eslint-config-typescript]() only for development: `pnpm i -D @happ/eslint-config-typescript`
4. Install [@happ/eslint-config-jest]() only for development: `pnpm i -D @happ/eslint-jest`
5. Install [@happ/eslint-config-angular]() only for development: `pnpm i -D @happ/eslint-config-angular`
6. Install [@happ/eslint-config-angular-template]() only for development: `pnpm i -D @happ/eslint-config-angular-template`
7. Install [@happ/eslint-config-json]() only for development: `pnpm i -D @happ/eslint-config-json`
8. Install [@happ/eslint-config-markdown]() only for development: `pnpm i -D @happ/eslint-config-markdown`
	 > Install it together: `pnpm i -D @happ/eslint-config @happ/eslint-config-typescript @happ/eslint-config-jest @happ/eslint-config-angular @happ/eslint-config-angular-template @happ/eslint-config-json @happ/eslint-config-markdown`
9. Create `.eslintrc.js` with:

	 <details>
		<summary>.eslintrc.js</summary>
	 
		 module.exports = {
			"overrides": [
				{
					"files": ["*.js", "*.ts"],
					"extends": ["@happ/eslint-config"]
				},
				{
					"files": ["*.ts"],
					"extends": ["@happ/eslint-config-typescript"]
				},
				{
					"files": ["*.spec.js", "*.spec.ts"],
					"extends": ["@happ/eslint-config-jest"]
				},
				{
					"files": ["ANGULAR_DIRECTORY/*.ts"],
					"extends": ["@happ/eslint-config-angular"]
				},
				{
					"files": ["ANGULAR_DIRECTORY/*.html"],
					"extends": ["@happ/eslint-config-angular-template"]
				},
				{
					"files": ["*.json"],
					"extends": ["@happ/eslint-config-json"]
				},
				{
					"files": ["*.md"],
					"extends": ["@happ/eslint-config-markdown"]
				}
			]
		 }
	 </details>

## Prettier

> [Prettier](https://www.npmjs.com/package/prettier)

1. Install [prettier](https://www.npmjs.com/package/prettier): `pnpm i -D prettier`
2. Install [@happ/prettier-config]() only for development: `pnpm i -D @happ/prettier-config`
3. Create `.prettierrc.js` with:

	<details>
		<summary>.prettierrc.js</summary>
 
		 module.exports = {
			extends: ["@happ/prettier-config"]
		 };
	</details>

## Stylelint

> [Stylelint](https://www.npmjs.com/package/stylelint)

1. Install [stylelint](https://www.npmjs.com/package/stylelint) only for development: `pnpm i -D stylelint`
2. Install [@happ/stylelint-config]() only for development: `pnpm i -D @happ/stylelint-config`
3. Create `.stylelintrc.js` with:

	<details>
		<summary>.stylelintrc.js</summary>
 
		 module.exports = {
			extends: ["@happ/stylelint-config"]
		 };
	</details>

## Editor config

> [Editor config](https://editorconfig.org/) 

1. Create `.editorconfig` with:

	 <details>
	 	<summary>.editorconfig</summary>

		 root = true
	
		 [*]
		 end_of_line = lf
		 insert_final_newline = true
		 indent_style = tab
		 indent_size = 2
	 </details>


> If you are using VS Code you have also install [plugin](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)


## Used libraries
1. [Npm-check](https://www.npmjs.com/package/npm-check)
2. [Husky](https://www.npmjs.com/package/husky)
3. [Commitlint](https://yarnpkg.com/package/commitlint)
4. [Commitizen](https://www.npmjs.com/package/commitizen)
5. [Cz-format-extension](https://www.npmjs.com/package/cz-format-extension)
6. [Conventional changelog cli](https://www.npmjs.com/package/conventional-changelog-cli)
7. [Eslint](https://www.npmjs.com/package/eslint)
8. [Prettier](https://www.npmjs.com/package/prettier)
9. [Stylelint](https://www.npmjs.com/package/stylelint)

## Next steps

1. To create a library run: `npx nx g @nrwl/workspace:lib LIB_NAME`
	 > 1. `LIB_NAME` - name of the library
2. To create an app you have to create a default project in app dir and then add it to:
	1. `nx.json` for `nx dependenices`
	2. `workspace.json` for `run|buid settings`

## Related projects:
1. [nx-web-starter](https://github.com/happ-agency/nx-web-starter)
2. [nx-nestjs-starter](https://github.com/happ-agency/nx-nestjs-starter)
3. [nx-angular-starter](https://github.com/happ-agency/nx-angular-starter)
4. [nx-angular-nestjs-starter](https://github.com/happ-agency/nx-angular-nestjs-starter)

## Additional info

> `workspace.json` and `angular.json` is the same. 
> 
> In `workspace.json` we use `version: 2` and `targets`, `generators`, `executor` 
> 
> In `angular.json` we use `version: 1` and `architect`, `schematics`, `builder`
