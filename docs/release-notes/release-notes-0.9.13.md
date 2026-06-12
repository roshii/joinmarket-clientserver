Joinmarket-clientserver 0.9.13:
=================

This release continues maintenance of the Joinmarket-clientserver codebase following the archival of the original upstream repository. The primary focus is security hardening, and dependency.

Upgrading
=========

To upgrade:

* Reminder: always back up and recreate your `joinmarket.cfg` file when upgrading, to ensure you receive any new default settings.

Run the `install.sh` script as described in the README and allow the existing `jmvenv` directory to be replaced when prompted.

Changes
=======

### Security

#### Mitigation of onion message flooding DoS attack

This release introduces several defenses against an attack where malicious peers connect directly to makers' onion services and flood them with requests, causing excessive logging, CPU usage, and memory consumption.

The protections include:

* Per-connection message rate limiting for inbound onion connections.
* Handshake requirements before processing Joinmarket protocol messages from non-directory peers.
* Reduced logging verbosity for expected failure conditions during attacks.
* Separate relaxed rate limits for outbound connections to directory nodes to avoid disrupting normal operation.

Comprehensive unit tests have been added to validate the new protections.

#### Security fixes via dependency updates

This release updates a number of dependencies to address known security vulnerabilities reported by GitHub Dependabot and upstream projects.

Notable issues addressed include:

* Multiple vulnerabilities in `cryptography`, including buffer overflow risks, incomplete certificate validation edge cases, vulnerable bundled OpenSSL versions, and an elliptic-curve subgroup validation issue.
* Multiple vulnerabilities in `pyOpenSSL`, including DTLS cookie callback buffer overflow and TLS connection validation bypass scenarios.
* A denial-of-service vulnerability in `Twisted`'s DNS protocol implementation (`twisted.names`).
* Multiple vulnerabilities in `Werkzeug`, including debugger remote code execution scenarios, multipart form parsing denial-of-service conditions, and Windows path handling issues.
* A JWT validation issue in `PyJWT` involving acceptance of unknown `crit` header extensions.
* A temporary-directory handling vulnerability in `pytest`.

### Project maintenance

* Removed the legacy `jmqtui` user interface.
* Cleaned up remaining references to `jmqt`.
* Removed unused Dockerfiles.
* Converted the project into a maintained fork.

### Dependency updates

Updated major dependencies to current supported releases, including:

* Twisted 24.7.0 → 26.4.0
* txtorcon 23.11.0 → 26.6.0
* cryptography 42.0.4 → 46.0.7
* pyOpenSSL 24.0.0 → 26.0.0
* Klein 20.6.0 → 24.8.0
* pytest 6.2.5 → 9.0.3
* Werkzeug 2.2.3 → 3.1.6
* PyJWT 2.4.0 → 2.12.0

### Build and platform support

* Removed Python 3.9 support.
* Updated CI configuration to test against modern dependency versions.
* Simplified unit test execution.
* Removed end-of-life macOS 13 build jobs.
* Optimized GitHub Actions workflows to run on pull requests and fail fast where appropriate.

### Documentation

This release contains minor maintenance and cleanup updates to project documentation and repository structure.

Credits
=======

Thanks to everyone who contributed to this release:

* @roshii
* @m0wer
* dependabot[bot]

And thanks to everyone who tested, reviewed, reported issues, and helped maintain the project.