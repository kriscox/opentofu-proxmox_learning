## Phase 4 — OpenTofu and Proxmox

1. OpenTofu manages desired infrastructure state through providers.

2. `tofu plan` shows the difference between:
   - the configuration;
   - the state;
   - the actual infrastructure.

3. `tofu apply` creates or updates infrastructure so that reality matches the desired configuration.

4. OpenTofu state contains:
   - explicitly configured values;
   - provider defaults;
   - values returned by the target platform, such as generated IDs or MAC addresses.

5. Infrastructure changes are not always destructive. Some properties can be updated in place, depending on the provider and target platform.

6. An `apply` is not necessarily transactional across all provider API operations. A partial change can already be applied before a later operation fails.

7. Proxmox permissions must be designed around the actual API operations:
   - VM administration rights do not automatically include pool management;
   - `Pool.Allocate` is required to manage VM membership in a pool;
   - image download and import through the Proxmox API can require broader system privileges such as `Sys.Modify`.

8. For this phase, Debian was provisioned from an existing installer ISO. The operating system installation was performed separately from OpenTofu, while OpenTofu managed the VM lifecycle itself.

9. The complete lifecycle exercised was:

   `init → plan → apply → inspect state → change → plan → apply → destroy`

10. Two common VM provisioning approaches are:
    - cloud-image based provisioning, which is better suited for full automation;
    - installer-ISO based provisioning, which can require fewer Proxmox privileges but introduces a separate OS installation step.

11. The basic OpenTofu lifecycle is:

   `init → plan → apply → inspect state → change → plan → apply → destroy`

## Future topics

- Automated OS provisioning using cloud images or unattended installation.
- Minimal custom Proxmox roles for automation identities.
- Image lifecycle and ownership.
- Remote state and locking.
