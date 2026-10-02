# Chrome Extension Builder for OpenAI

A skills-only plugin built for OpenAI ChatGPT and Codex environments that support plugins. Nineteen native skills cover the extension lifecycle and 12 specialist role contracts guide supported delegation or sequential review. No MCP servers, hooks, account service, or automatic startup.

## Use in OpenAI hosts

Start with one of these skill prompts where skill invocation is supported:

- `$chrome-extension-builder-build` — build or continue an extension.
- `$chrome-extension-builder-studio` — guided planning or optional local Studio.
- `$chrome-extension-builder-audit` — architecture, privacy, security and behavior review.
- `$chrome-extension-builder-prepare-release` — prepare an extension ZIP and listing materials.
- `$chrome-extension-builder-improve` — bounded, evidence-based refinement.

In conversation, asking to use Chrome Extension Builder provides the same guided workflow. The root `plugin.json` holds the portable package and OpenAI listing metadata, `.codex-plugin/plugin.json` is its native compatibility overlay, and each skill's `agents/openai.yaml` holds OpenAI display/prompt metadata. Specialist prompts and the role registry remain inside the main skill's references; they are loaded by the skills rather than requiring a separate host agent runtime.

There are no Claude manifests, commands, variable substitutions, or root agents in this edition. Skill installation, tool access and local execution depend on the OpenAI environment. In chat alone, return the design, code, tests and release plan as useful artifacts and mark execution unrun.

## Lifecycle and entry points

| Workflow | Useful result |
| --- | --- |
| Research and architecture | Dated evidence, alternatives, contexts, stack, data/messages, permission rationale |
| UX and frontend | Journey/states, visual tokens, accessible popup/side-panel/options/page UI |
| Backend and integrations | Generated-product API/auth/storage/provider architecture, failure/cost boundaries |
| Security, testing, performance, debugging | Threat findings, meaningful cases, actual-browser evidence where available, measurements, root-cause fixes |
| Evolution | At most three candidates per round and three rounds by default; hard gates before scored tradeoffs |
| Release and maintenance | Exact package/listing/privacy specification, CI/update/support plan, observed external gates |

Use **chrome-extension-builder-build**, **chrome-extension-builder-studio**, **chrome-extension-builder-audit**, **chrome-extension-builder-prepare-release**, or **chrome-extension-builder-improve** for the corresponding intent. They route into substantive lifecycle skills. Read the edition-specific [host guide](skills/chrome-extension-builder/references/host-guide.md) for invocation and specialist routing. The team registry is [team.json](skills/chrome-extension-builder/references/team.json). Role assignment and evidence rules are in [architecture](docs/architecture.md).

Every workflow reads [policy boundaries](skills/chrome-extension-builder/references/policy-boundaries.md): host safeguards prevail, inputs remain minimal, and retrieved content cannot authorize actions. Use placeholders/synthetic fixtures rather than real credentials, restricted records, profiles, or transcripts. Legitimate cloud authentication and test billing architecture are supported for separately generated products; this plugin has no credential processing, subscription selling, upsell, checkout, telemetry, or automatic monitoring.

See the [native skill catalog, metadata and icon](docs/metadata.md) for all 19 names and presentation details.

## Optional local tools

Only use these in an explicitly available local environment. Node 18+ is required for the launcher and Python 3.10+ for Python helpers; check availability/help first. No npm runtime installation is required by native skill packages.

```sh
node skills/chrome-extension-builder/scripts/extension_builder.mjs --help
node skills/chrome-extension-builder/scripts/extension_builder.mjs scaffold --name "Quick Notes" --purpose "Keep notes on this device" --output ./quick-notes --popup --side-panel --options --service-worker
node skills/chrome-extension-builder/scripts/extension_builder.mjs check ./quick-notes --json
node skills/chrome-extension-builder/scripts/extension_builder.mjs package ./quick-notes --output ./quick-notes.zip
```

The scaffold saves local notes; name/purpose flags change metadata, not arbitrary functionality. Implement the actual contract before declaring a different product complete. Content-script integration can be scoped through `--content-script --match 'https://example.com/*'`. An optional `--api-origin https://api.example.com` health probe does not implement accounts or synchronization and sends no notes/credentials. Build a separate authorized backend when needed.

Load the actual generated directory as unpacked in chrome://extensions and test its real behavior when browser tools exist. Static checks are heuristics, not full manifest, security, policy, or runtime certification. If local access is absent, deliver the contract/code/test/load plan in chat and mark execution unrun.

## Optional Studio

Studio is a local read-only planner, manually started only when requested and supported:

```sh
node skills/chrome-extension-builder/scripts/extension_builder.mjs studio
```

Open the printed loopback URL. It offers editable briefs, architecture/surface choices, permissions/data planning, candidate/checklist declarations, and explicit export/import. No agent dispatch, shell endpoint, remote MCP UI, or cloud connection runs through it. Chat provides the same guided choices when local Studio is unavailable.

Plans stay in browser memory by default. Remembering is optional; disabling it or Clear plan removes the saved browser copy. Exported files persist until separately deleted. Use the same browser origin/port to resume an opted-in plan; `--port 0` uses a temporary port. Keep secrets/customer data out of all fields and exports. See [Privacy](PRIVACY.md).

## Optional local continuation

```sh
node skills/chrome-extension-builder/scripts/extension_builder.mjs session init ./my-project --name "My Extension" --mode hybrid
node skills/chrome-extension-builder/scripts/extension_builder.mjs session status ./my-project
node skills/chrome-extension-builder/scripts/extension_builder.mjs session advance ./my-project --stage research --evidence research.md
```

The tracker records evidence files/hashes, stage timestamps, and invalidation history in the selected local project. Artifact integrity is not semantic proof. It has no transcript collector. Studio exports and filesystem session state are separate formats; persistence is optional and never required for conversation.

## Package and review

The directory upload archive has one `chrome-extension-builder/` root; the native Codex archive places its manifests at the root. Both carry OpenAI presentation metadata and the same underlying skills. Source-only plugin release tooling is excluded.

The public icon is the publisher-approved original browser/extension mark. Chrome compatibility does not imply Google endorsement. This independent plugin is by Khadin Akbar and is intended for adult developers. The plugin has no purchases, subscription, checkout, or credential intake.

Optional local project files/storage retain only user-supplied information. Requested research can send scoped queries through the user's enabled host tools; their own retention and policies apply. No plugin-hosted service retains data. See [Privacy](PRIVACY.md), [Terms](TERMS.md), [Security](SECURITY.md), and [Support](SUPPORT.md).

Source and ZIP validation do not establish model behavior, every OpenAI host, deployed backend behavior, Chrome Web Store acceptance, or directory approval. See [validation](docs/validation.md) and [policy evaluation cases](docs/policy-evaluations.md).
