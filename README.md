# Personal HomeLab kubernetes configuration
This repository leverages fluxcd to automatically sync cluster configuration and configure custom applications
Secrets are managed with sealedsecrets.

Initial setup requires flux to be setup once and then the bootstrap can reconfigure itself with a stored flux instilation.
