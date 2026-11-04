<!-- markdownlint-disable -->

# Hardening Report: r0adkll--upload-google-play/v1.1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **r0adkll--upload-google-play/v1.1.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed lib/index.js without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/lib/index.js b/lib/index.js
index 590dab4..691ea1c 100644
--- a/lib/index.js
+++ b/lib/index.js
@@ -1,40 +1,42 @@
-(()=>{var __webpack_modules__={7351:function(e,t,r){"use strict";var a=this&&this.__createBinding||(Object.create?function(e,t,r,a){if(a===undefined)a=r;Object.defineProperty(e,a,{enumerable:true,get:function(){return t[r]}})}:function(e,t,r,a){if(a===undefined)a=r;e[a]=t[r]});var i=this&&this.__setModuleDefault||(Object.create?function(e,t){Object.defineProperty(e,"default",{enumerable:true,value:t})}:function(e,t){e["default"]=t});var n=this&&this.__importStar||function(e){if(e&&e.__esModule)return e;var t={};if(e!=null)for(var r in e)if(r!=="default"&&Object.hasOwnProperty.call(e,r))a(t,e,r);i(t,e);return t};Object.defineProperty(t,"__esModule",{value:true});t.issue=t.issueCommand=void 0;const s=n(r(2037));const o=r(5278);function issueCommand(e,t,r){const a=new Command(e,t,r);process.stdout.write(a.toString()+s.EOL)}t.issueCommand=issueCommand;function issue(e,t=""){issueCommand(e,{},t)}t.issue=issue;const p="::";class Command{constructor(e,t,r){if(!e){e="missing.command"}this.command=e;this.properties=t;this.message=r}toString(){let e=p+this.command;if(this.properties&&Object.keys(this.properties).length>0){e+=" ";let t=true;for(const r in this.properties){if(this.properties.hasOwnProperty(r)){const a=this.properties[r];if(a){if(t){t=false}else{e+=","}e+=`${r}=${escapeProperty(a)}`}}}}e+=`${p}${escapeData(this.message)}`;return e}}function escapeData(e){return o.toCommandValue(e).replace(/%/g,"%25").replace(/\r/g,"%0D").replace(/\n/g,"%0A")}function escapeProperty(e){return o.toCommandValue(e).replace(/%/g,"%25").replace(/\r/g,"%0D").replace(/\n/g,"%0A").replace(/:/g,"%3A").replace(/,/g,"%2C")}},2186:function(e,t,r){"use strict";var a=this&&this.__createBinding||(Object.create?function(e,t,r,a){if(a===undefined)a=r;Object.defineProperty(e,a,{enumerable:true,get:function(){return t[r]}})}:function(e,t,r,a){if(a===undefined)a=r;e[a]=t[r]});var i=this&&this.__setModuleDefault||(Object.create?function(e,t){Object.defineProperty(e,"default",{enumerable:true,value:t})}:function(e,t){e["default"]=t});var n=this&&this.__importStar||function(e){if(e&&e.__esModule)return e;var t={};if(e!=null)for(var r in e)if(r!=="default"&&Object.hasOwnProperty.call(e,r))a(t,e,r);i(t,e);return t};var s=this&&this.__awaiter||function(e,t,r,a){function adopt(e){return e instanceof r?e:new r((function(t){t(e)}))}return new(r||(r=Promise))((function(r,i){function fulfilled(e){try{step(a.next(e))}catch(e){i(e)}}function rejected(e){try{step(a["throw"](e))}catch(e){i(e)}}function step(e){e.done?r(e.value):adopt(e.value).then(fulfilled,rejected)}step((a=a.apply(e,t||[])).next())}))};Object.defineProperty(t,"__esModule",{value:true});t.getIDToken=t.getState=t.saveState=t.group=t.endGroup=t.startGroup=t.info=t.notice=t.warning=t.error=t.debug=t.isDebug=t.setFailed=t.setCommandEcho=t.setOutput=t.getBooleanInput=t.getMultilineInput=t.getInput=t.addPath=t.setSecret=t.exportVariable=t.ExitCode=void 0;const o=r(7351);const p=r(717);const d=r(5278);const l=n(r(2037));const u=n(r(1017));const c=r(8041);var m;(function(e){e[e["Success"]=0]="Success";e[e["Failure"]=1]="Failure"})(m=t.ExitCode||(t.ExitCode={}));function exportVariable(e,t){const r=d.toCommandValue(t);process.env[e]=r;const a=process.env["GITHUB_ENV"]||"";if(a){return p.issueFileCommand("ENV",p.prepareKeyValueMessage(e,t))}o.issueCommand("set-env",{name:e},r)}t.exportVariable=exportVariable;function setSecret(e){o.issueCommand("add-mask",{},e)}t.setSecret=setSecret;function addPath(e){const t=process.env["GITHUB_PATH"]||"";if(t){p.issueFileCommand("PATH",e)}else{o.issueCommand("add-path",{},e)}process.env["PATH"]=`${e}${u.delimiter}${process.env["PATH"]}`}t.addPath=addPath;function getInput(e,t){const r=process.env[`INPUT_${e.replace(/ /g,"_").toUpperCase()}`]||"";if(t&&t.required&&!r){throw new Error(`Input required and not supplied: ${e}`)}if(t&&t.trimWhitespace===false){return r}return r.trim()}t.getInput=getInput;function getMultilineInput(e,t){const r=getInput(e,
... (truncated)
```

Locations:

- `lib/index.js`

## Iteration Notes

### Iteration 1

**Fixes applied:** prior-fix

**Notes:**

The prior patch shown in the finding was cut off after the start of line 1. Its hunk header (-1,40 +1,42) means it rewrote the whole 40-line webpack bundle, so I couldn't tell from it what it changed for security. lib/index.js is a 949KB minified file I can't read directly, so I located code by regex search instead. Checks done: action.yml is a plain node24 action with no run steps or uses: lines; src/ has no child_process, exec or shell use; the bundle still uses current @actions/core file commands (GITHUB_ENV/GITHUB_PATH with random delimiters). The one security-relevant spot is where the action writes the serviceAccountJsonPlainText credential to ./serviceAccountJson.json. Change made: that file is now created owner-only (mode 0o600, written as mode:384 in the bundle), in both lib/index.js and src/main.ts. Behaviour is otherwise unchanged: same path, same GOOGLE_APPLICATION_CREDENTIALS export, same cleanup. I couldn't confirm this matches what the earlier harden changed, so a reviewer with the full prior diff should check whether it did anything more.

