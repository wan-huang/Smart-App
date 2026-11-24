# SMART Patient App

A patient-facing SMART on FHIR app for GitHub Pages. The patient opens the app, signs in against the SMART Health IT R4 sandbox, and the app reads their Patient resource.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | App home and OAuth redirect target. Calls `FHIR.oauth2.ready()` and shows name, gender, birth date, and age. |
| `launch.html` | Patient standalone launch. Calls `FHIR.oauth2.authorize()`. |
| `health.html` | Static hosting smoke check. |
| `.nojekyll` | Serves the files as-is on GitHub Pages. |
| `README.md` | Publishing instructions and how to sign in. |

## Publish and verify

1. Put these files, including `.nojekyll`, at the root of a GitHub project repository and push them to `main`.
2. In **Settings → Pages → Build and deployment**, select **Deploy from a branch**, then **main** and **/(root)**. Save.
3. After deployment, open `launch.html`. The SMART sandbox asks you to sign in as a patient. After you approve access, the app opens `index.html` and shows that patient's name, gender, birth date, and age.

| Page | Default GitHub Pages URL |
| --- | --- |
| App, after sign-in | `https://<owner>.github.io/<repo>/` |
| Health check | `https://<owner>.github.io/<repo>/health.html` |
| Patient sign-in | `https://<owner>.github.io/<repo>/launch.html` |

These URLs assume a project site with the default domain. A repository named `<owner>.github.io` publishes at `https://<owner>.github.io/`, with the file paths directly under that root. [GitHub Pages setup](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Patient sign-in

`launch.html` starts a standalone launch at the [SMART Health IT R4 sandbox](https://launch.smarthealthit.org/). The scope is `launch/patient openid fhirUser patient/Patient.read`, so the sandbox asks which patient is signing in and the app can read that Patient resource. The sandbox sends the browser back to `index.html`, and `FHIR.oauth2.ready()` exchanges the authorization code for an access token. [HL7 SMART App Launch](https://hl7.org/fhir/smart-app-launch/app-launch.html)
