# Security policy

Report vulnerabilities privately through GitHub's "Report a vulnerability" (Security tab) of
hackin2minutes-oss/sawone-action. Please do not open a public issue. You will get an answer within a week.

This repository contains the Sawone action and reusable workflows only. They pull the signed engine image
(`ghcr.io/hackin2minutes-oss/sawone-scanner`) and verify its Sigstore signature before running. The scan runs
scanners as sibling containers on the runner's Docker daemon: use it on ephemeral runners (GitHub-hosted or
equivalent).
