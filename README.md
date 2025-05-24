# Container Images
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-8-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

This repository is a fork of the now-discontinued [k8s-at-home/container-images](https://github.com/k8s-at-home/container-images) project. It contains a curated selection of container images tailored for Kubernetes, which are personally used and maintained. Images are hosted on Github Container Registry [here](https://github.com/orgs/k8s-at-home/packages?ecosystem=container&visibility=public).

## Selected Container Images

- [emby](./apps/emby/)
- [jackett](./apps/jackett/)
- [kubectl](./apps/kubectl/)
- [plex](./apps/plex/)
- [plex-pass](./apps/plex-pass/)
- [podsync](./apps/podsync/)
- [qbittorrent](./apps/qbittorrent/)
- [radarr](./apps/radarr/)
- [sonarr](./apps/sonarr/)
- [tt-rss](./apps/tt-rss/)
- [udp-broadcast-relay-redux](./apps/udp-broadcast-relay-redux/)
- [wikijs](./apps/wikijs/)
- [wireguard](./apps/wireguard/)

## Automated Image Building Workflow

This project uses GitHub Actions to automate the building, testing, and updating of container images. The workflow is primarily managed by two files:

### `release.yaml`
This workflow is responsible for building and publishing the container images. It is triggered under the following conditions:
- When changes are pushed to the `main` branch within the `apps/` or `base/` directories.
- Manually, via the `workflow_dispatch` event on GitHub.

The key steps in this workflow include:
- **Detecting Changes:** Identifies which container image definitions have been modified.
- **Linting:** Uses Hadolint to check the `Dockerfile` for common errors and best practice violations.
- **Building Images:** Builds container images for the platforms specified in the `PLATFORM` file and versions from the `VERSION` file located within each image's directory.
- **Testing (GOSS):** If a `goss.yaml` file is present in the image's directory, [GOSS](https://github.com/goss-org/goss) tests are run against the built image to ensure its integrity and functionality.
- **Publishing:** Pushes successfully built and tested images to Github Container Registry (GHCR). Images are tagged with `latest`, `rolling`, and a specific version tag (e.g., `v1.2.3`).

### `schedule.yaml`
This workflow helps keep the application versions up-to-date.
- It runs on a predefined schedule (e.g., every 12 hours) and can also be triggered manually.
- For each application in the `apps/` and `base/` directories, it executes a `latest-version.sh` script (if present).
- These scripts are designed to fetch the latest available version of the application from its source.
- If a new version is found, the `VERSION` file within the respective image's directory is updated.
- This update to the `VERSION` file, when pushed to the `main` branch, subsequently triggers the `release.yaml` workflow to build and publish the new version of the container image.

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://schouten-lebbing.nl"><img src="https://avatars.githubusercontent.com/u/7613738?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Kjeld Schouten-Lebbing</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=Ornias1993" title="Code">💻</a></td>
    <td align="center"><a href="https://nicholaswilde.github.io/"><img src="https://avatars.githubusercontent.com/u/600019?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Nicholas Wilde</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=nicholaswilde" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/angelnu"><img src="https://avatars.githubusercontent.com/u/4406403?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Vegetto</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=angelnu" title="Code">💻</a></td>
    <td align="center"><a href="http://anthonyrabbito.com"><img src="https://avatars.githubusercontent.com/u/25143877?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Anthony Rabbito</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=anthr76" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/bjw-s"><img src="https://avatars.githubusercontent.com/u/6213398?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Bᴇʀɴᴅ Sᴄʜᴏʀɢᴇʀs</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=bjw-s" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/onedr0p"><img src="https://avatars.githubusercontent.com/u/213795?v=4?s=100" width="100px;" alt=""/><br /><sub><b>ᗪєνιη ᗷυнʟ</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=onedr0p" title="Code">💻</a></td>
    <td align="center"><a href="https://cajun.pro"><img src="https://avatars.githubusercontent.com/u/15788890?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Nicholas St. Germain</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=DirtyCajunRice" title="Code">💻</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/djs52"><img src="https://avatars.githubusercontent.com/u/1466018?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Dan Sheridan</b></sub></a><br /><a href="https://github.com/k8s-at-home/container-images/commits?author=djs52" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
