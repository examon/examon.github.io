# In-place upgrade workflow

| Phase         | Description |
| ------------- |:-------------:|
| Facts Collection | <li>Operating System Version Detection, IP, Hostname, RPMs, Services, Augeas run</li> |
| Checks | <li>**Preupgrade Checks** (Inhibitors - Blockers, Shared Objects, Binaries, Languages, Packages, Load Balance Support, User Management, Version Control Systems, FreeRADIUS, IPA Bind Dyndb LDAP, SSSD, NTP, OpenLDAP, YPSERV, Network, Databases, SELinux, Storage, System)</li> <li>**Services** (HTTPD, OpenSSH, Postfix, SQUID, DoveCot, Bind9 Configuration)</li> <li>**Backup** (Untracked Files)</li> <li>**Others** (RSYSLOG)</li>|
| Report | <li>Provide user with the result of the checks</li><li>Let user interactively decide on multiple-choice solution for specific upgrade issues</li>|
| Attach package repositories | <li>Make sure the repositories of the new system are available</li> |
| Planning | <li>RPM Install transaction (feasibility checks)</li> |
| Download | <li>Download of all things needed (RPMs, Kernel images, Anaconda image (very big maybe), etc.)</li> |
| Upgrade RamDisk Preparation | <li>Preparation of initial ramdisk (if required)</li> <li>Setup bootloaderGrub</li> |
| **`UPGRADE RAMDISK FROM HERE`** | |
| Upgrade RamDisk Start (Actual reboot) | <li>Reboot into the next system therefore not a real step, however the before and post parts are interesting to have for hooking</li> |
| Network | <li>Bring up the network</li> |
| Storage | <li>Mount all storage points</li> |
| Late Tests | <li>Tests that need to be executed later</li> |
| **`POINT OF NO RETURN`** | |
| Preparation | <li>YUM Configurations</li> <li>Backup not upgradable configurations (No Verify Configs)</li> |
| RPM Upgrade | <li>Upgrade RPMs</li> <li>Check all files are installed (troubles with handling dirs/symlinks), includes reinstallation of affected packages</li> |
| Application Upgrade | <li>Application of changes on configuration files, move various directores, etc.</li> |
| Third Party Applications | <li>A place for custom actors for third party applications to be upgraded</li> |
| Finalization | <li>Plan SELinux relabeling</li> <li>Labels Bootloader settings</li> |
| Reboot | <li>Reboot into the new system</li> |
| **`UPGRADED SYSTEM FROM HERE`** | |
| First Boot | |
