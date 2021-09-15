# Red Hat Package Manager RPM

---

## What is an RMP package?

RPM is a popular package management tool in Red Hat Enterprise Linux-based distros. Using RPM, you can install, uninstall, and query individual software packages. Still, it cannot manage dependency resolution like YUM. RPM does provide you useful output, including a list of required packages. An RPM package consists of an archive of files and metadata. Metadata includes helper scripts, file attributes, and information about packages.

## What is a dependency in Linux?

A dependency occurs when one package depends on another. You might think it would make for an easier-to-manage system if no package depended on any others, but you’d face a few problems, not the least of which would be dramatically increased disk usage.

## What is a repository in Linux?

A Linux repository is a storage location from which your system retrieves and installs OS updates and applications. Each repository is a collection of software hosted on a remote server and intended to be used for installing and updating software packages on Linux systems.

On RedHat, Fedora and similar systems, you would use a command like the one shown below to view the repositories that your update commands use. Note that we're using the dnf command in this example. This is the replacement for the older yum command.

```bash
[root@6b6ff9f9bc2d /]# sudo dnf repolist
repo id                        repo name
fedora                         Fedora 34 - x86_64
fedora-cisco-openh264          Fedora 34 openh264 (From Cisco) - x86_64
fedora-modular                 Fedora Modular 34 - x86_64
updates                        Fedora 34 - x86_64 - Updates
updates-modular                Fedora Modular 34 - x86_64 - Updates
```

## Install an RPM package, document the process

```bash
# We are using Fedora
# There are differents methods to get an RPM file, such as download directly
# the RPM file or download using a link as per below.
# In this case we will download Google Chrome using this link and wget command
# https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm

[root@c80ced9a3596 /]# wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm 
--2021-09-03 14:56:23--  https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
Resolving dl.google.com (dl.google.com)... 142.251.34.78, 2607:f8b0:4012:815::200e
Connecting to dl.google.com (dl.google.com)|142.251.34.78|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 82638560 (79M) [application/x-rpm]
Saving to: ‘google-chrome-stable_current_x86_64.rpm’

google-chrome-stable_c 100%[============================>]  78.81M  4.34MB/s    in 1m 41s  

2021-09-03 14:58:04 (801 KB/s) - ‘google-chrome-stable_current_x86_64.rpm’ saved [82638560/82638560]

# Installing donwloaded file 
# In this firs part dependencies are installed to avoid issues
# and then we have to wait until see "Complete!" message

[root@c80ced9a3596 /]# sudo dnf install google-chrome-stable_current_x86_64.rpm
Last metadata expiration check: 0:35:41 ago on Fri Sep  3 14:37:08 2021.
Dependencies resolved.
============================================================================================
 Package                    Arch      Version                         Repository       Size
============================================================================================
Installing:
 google-chrome-stable       x86_64    93.0.4577.63-1                  @commandline     79 M
Installing dependencies:
 acl                        x86_64    2.3.1-1.fc34                    fedora           71 k
 adwaita-cursor-theme       noarch    40.1.1-1.fc34                   updates         625 k
 adwaita-icon-theme         noarch    40.1.1-1.fc34                   updates          11 M
 alsa-lib                   x86_64    1.2.5.1-2.fc34                  updates         492 k
 at-spi2-atk                x86_64    2.38.0-2.fc34                   fedora           90 k
 at-spi2-core               x86_64    2.40.3-1.fc34                   updates         176 k
 atk                        x86_64    2.36.0-3.fc34                   fedora          273 k
 avahi-libs                 x86_64    0.8-14.fc34                     updates          68 k
 cairo                      x86_64    1.17.4-3.fc34                   fedora          671 k
 cairo-gobject              x86_64    1.17.4-3.fc34                   fedora           18 k
 colord-libs                x86_64    1.4.5-2.fc34                    fedora          240 k
 cpio                       x86_64    2.13-10.fc34                    fedora          274 k
 crypto-policies-scripts    noarch    20210213-1.git5c710c0.fc34      fedora           65 k
 cryptsetup-libs            x86_64    2.3.6-1.fc34                    updates         474 k
 cups-libs                  x86_64    1:2.3.3op2-7.fc34               updates         276 k
 dbus                       x86_64    1:1.12.20-3.fc34                fedora          8.0 k
 dbus-broker                x86_64    29-2.fc34                       updates         172 k
 dbus-common                noarch    1:1.12.20-3.fc34                fedora           15 k
 dbus-libs                  x86_64    1:1.12.20-3.fc34                fedora          151 k
 desktop-file-utils         x86_64    0.26-3.fc34                     fedora           74 k
 device-mapper              x86_64    1.02.175-1.fc34                 fedora          144 k
 device-mapper-libs         x86_64    1.02.175-1.fc34                 fedora          179 k
 dracut                     x86_64    055-3.fc34                      updates         347 k
 emacs-filesystem           noarch    1:27.2-5.fc34                   updates         8.4 k
 file                       x86_64    5.39-6.fc34                     updates          50 k
 findutils                  x86_64    1:4.8.0-2.fc34                  fedora          545 k
 flac-libs                  x86_64    1.3.3-7.fc34                    fedora          220 k
 fontconfig                 x86_64    2.13.94-2.fc34                  updates         273 k
 freetype                   x86_64    2.10.4-3.fc34                   fedora          394 k
 fribidi                    x86_64    1.0.10-4.fc34                   fedora           86 k
 fuse-libs                  x86_64    2.9.9-11.fc34                   fedora           99 k
 gdk-pixbuf2                x86_64    2.42.6-1.fc34                   updates         471 k
 gdk-pixbuf2-modules        x86_64    2.42.6-1.fc34                   updates          85 k
 gettext                    x86_64    0.21-4.fc34                     fedora          1.1 M
 gettext-libs               x86_64    0.21-4.fc34                     fedora          313 k
 graphite2                  x86_64    1.3.14-7.fc34                   fedora           95 k
 grub2-common               noarch    1:2.06-2.fc34                   updates         924 k
 grub2-tools                x86_64    1:2.06-2.fc34                   updates         1.8 M
 grub2-tools-minimal        x86_64    1:2.06-2.fc34                   updates         604 k
 gsm                        x86_64    1.0.19-5.fc34                   updates          33 k
 gstreamer1                 x86_64    1.19.1-2.1.18.4.fc34            updates         1.4 M
 gtk-update-icon-cache      x86_64    3.24.30-1.fc34                  updates          35 k
 gtk3                       x86_64    3.24.30-1.fc34                  updates         4.8 M
 harfbuzz                   x86_64    2.7.4-3.fc34                    fedora          634 k
 hicolor-icon-theme         noarch    0.17-10.fc34                    fedora           45 k
 hwdata                     noarch    0.351-1.fc34                    updates         1.5 M
 iptables-legacy-libs       x86_64    1.8.7-8.fc34                    updates          40 k
 jbigkit-libs               x86_64    2.1-21.fc34                     fedora           53 k
 kbd                        x86_64    2.4.0-2.fc34                    fedora          390 k
 kbd-misc                   noarch    2.4.0-2.fc34                    fedora          1.5 M
 kmod                       x86_64    29-2.fc34                       updates         114 k
 kmod-libs                  x86_64    29-2.fc34                       updates          63 k
 lcms2                      x86_64    2.12-1.fc34                     fedora          171 k
 libICE                     x86_64    1.0.10-6.fc34                   fedora           71 k
 libSM                      x86_64    1.2.3-8.fc34                    fedora           42 k
 libX11                     x86_64    1.7.2-3.fc34                    updates         646 k
 libX11-common              noarch    1.7.2-3.fc34                    updates         152 k
 libX11-xcb                 x86_64    1.7.2-3.fc34                    updates          11 k
 libXau                     x86_64    1.0.9-6.fc34                    fedora           31 k
 libXcomposite              x86_64    0.4.5-5.fc34                    fedora           23 k
 libXcursor                 x86_64    1.2.0-5.fc34                    fedora           30 k
 libXdamage                 x86_64    1.1.5-5.fc34                    fedora           22 k
 libXext                    x86_64    1.3.4-6.fc34                    fedora           39 k
 libXfixes                  x86_64    6.0.0-1.fc34                    updates          19 k
 libXft                     x86_64    2.3.3-6.fc34                    fedora           63 k
 libXi                      x86_64    1.7.10-6.fc34                   fedora           39 k
 libXinerama                x86_64    1.1.4-8.fc34                    fedora           14 k
 libXrandr                  x86_64    1.5.2-6.fc34                    fedora           28 k
 libXrender                 x86_64    0.9.10-14.fc34                  fedora           27 k
 libXtst                    x86_64    1.2.3-14.fc34                   fedora           20 k
 libargon2                  x86_64    20171227-6.fc34                 fedora           29 k
 libasyncns                 x86_64    0.8-20.fc34                     fedora           30 k
 libcanberra                x86_64    0.30-24.fc34                    fedora           87 k
 libcloudproviders          x86_64    0.3.1-3.fc34                    fedora           46 k
 libdatrie                  x86_64    0.2.13-1.fc34                   fedora           32 k
 libdrm                     x86_64    2.4.107-1.fc34                  updates         162 k
 libedit                    x86_64    3.1-38.20210714cvs.fc34         updates         104 k
 libepoxy                   x86_64    1.5.9-1.fc34                    updates         243 k
 liberation-fonts           noarch    1:2.1.4-1.fc34                  updates         8.2 k
 liberation-fonts-common    noarch    1:2.1.4-1.fc34                  updates          15 k
 liberation-mono-fonts      noarch    1:2.1.4-1.fc34                  updates         501 k
 liberation-sans-fonts      noarch    1:2.1.4-1.fc34                  updates         607 k
 liberation-serif-fonts     noarch    1:2.1.4-1.fc34                  updates         605 k
 libevent                   x86_64    2.1.12-3.fc34                   fedora          268 k
 libgusb                    x86_64    0.3.7-1.fc34                    updates          49 k
 libibverbs                 x86_64    36.0-1.fc34                     updates         354 k
 libjpeg-turbo              x86_64    2.0.90-2.fc34                   fedora          176 k
 libkcapi                   x86_64    1.2.1-1.fc34                    fedora           43 k
 libkcapi-hmaccalc          x86_64    1.2.1-1.fc34                    fedora           24 k
 libnl3                     x86_64    3.5.0-6.fc34                    fedora          324 k
 libogg                     x86_64    2:1.3.4-4.fc34                  fedora           33 k
 libpcap                    x86_64    14:1.10.1-1.fc34                updates         171 k
 libpciaccess               x86_64    0.16-4.fc34                     fedora           27 k
 libpng                     x86_64    2:1.6.37-10.fc34                fedora          119 k
 libseccomp                 x86_64    2.5.0-4.fc34                    fedora           71 k
 libsndfile                 x86_64    1.0.31-5.fc34.fc34              updates         206 k
 libtdb                     x86_64    1.4.3-6.fc34                    fedora           51 k
 libtextstyle               x86_64    0.21-4.fc34                     fedora           91 k
 libthai                    x86_64    0.1.28-6.fc34                   fedora          213 k
 libtiff                    x86_64    4.2.0-1.fc34                    fedora          194 k
 libtool-ltdl               x86_64    2.4.6-40.fc34                   fedora           36 k
 libunwind                  x86_64    1.4.0-5.fc34                    fedora           65 k
 libvorbis                  x86_64    1:1.3.7-3.fc34                  fedora          199 k
 libwayland-client          x86_64    1.19.0-1.fc34                   fedora           32 k
 libwayland-cursor          x86_64    1.19.0-1.fc34                   fedora           19 k
 libwayland-egl             x86_64    1.19.0-1.fc34                   fedora           12 k
 libwayland-server          x86_64    1.19.0-1.fc34                   fedora           41 k
 libwebp                    x86_64    1.2.1-1.fc34                    updates         279 k
 libxcb                     x86_64    1.13.1-7.fc34                   fedora          230 k
 libxkbcommon               x86_64    1.3.0-1.fc34                    updates         144 k
 libxshmfence               x86_64    1.3-8.fc34                      fedora           12 k
 llvm-libs                  x86_64    12.0.1-1.fc34                   updates          23 M
 mesa-libgbm                x86_64    21.1.7-1.fc34                   updates          42 k
 mesa-vulkan-drivers        x86_64    21.1.7-1.fc34                   updates         4.8 M
 nspr                       x86_64    4.32.0-1.fc34                   updates         138 k
 nss                        x86_64    3.69.0-1.fc34                   updates         684 k
 nss-softokn                x86_64    3.69.0-1.fc34                   updates         378 k
 nss-softokn-freebl         x86_64    3.69.0-1.fc34                   updates         324 k
 nss-sysinit                x86_64    3.69.0-1.fc34                   updates          21 k
 nss-util                   x86_64    3.69.0-1.fc34                   updates          88 k
 opus                       x86_64    1.3.1-8.fc34                    fedora          202 k
 os-prober                  x86_64    1.77-7.fc34                     fedora           44 k
 pango                      x86_64    1.48.9-2.fc34                   updates         299 k
 pixman                     x86_64    0.40.0-3.fc34                   fedora          274 k
 procps-ng                  x86_64    3.3.17-1.fc34.1                 updates         334 k
 pulseaudio-libs            x86_64    14.2-3.fc34                     fedora          728 k
 sound-theme-freedesktop    noarch    0.8-15.fc34                     fedora          378 k
 systemd                    x86_64    248.7-1.fc34                    updates         4.4 M
 systemd-pam                x86_64    248.7-1.fc34                    updates         320 k
 systemd-rpm-macros         noarch    248.7-1.fc34                    updates          28 k
 systemd-udev               x86_64    248.7-1.fc34                    updates         1.5 M
 vulkan-loader              x86_64    1.2.162.0-2.fc34                fedora          126 k
 which                      x86_64    2.21-26.fc34                    updates          42 k
 xdg-utils                  noarch    1.1.3-9.fc34                    updates          72 k
 xkeyboard-config           noarch    2.33-1.fc34                     updates         783 k
 xml-common                 noarch    0.6.3-56.fc34                   fedora           31 k
 xz                         x86_64    5.2.5-5.fc34                    fedora          216 k
Installing weak dependencies:
 dconf                      x86_64    0.40.0-3.fc34                   updates         110 k
 diffutils                  x86_64    3.7-8.fc34                      fedora          391 k
 grubby                     x86_64    8.40-51.fc34                    fedora           36 k
 kpartx                     x86_64    0.8.5-4.fc34                    fedora           49 k
 libcanberra-gtk3           x86_64    0.30-24.fc34                    fedora           32 k
 memstrack                  x86_64    0.2.2-1.fc34                    fedora           50 k
 pigz                       x86_64    2.5-1.fc34                      fedora           82 k
 qrencode-libs              x86_64    4.0.2-7.fc34                    fedora           60 k
 systemd-networkd           x86_64    248.7-1.fc34                    updates         476 k

Transaction Summary
============================================================================================
Install  147 Packages

Total size: 159 M
Total download size: 81 M
Installed size: 537 M
Is this ok [y/N]: y
Downloading Packages:
(1/146): acl-2.3.1-1.fc34.x86_64.rpm                         79 kB/s |  71 kB     00:00    
(2/146): at-spi2-atk-2.38.0-2.fc34.x86_64.rpm                98 kB/s |  90 kB     00:00    
(3/146): cairo-gobject-1.17.4-3.fc34.x86_64.rpm              56 kB/s |  18 kB     00:00    
(4/146): atk-2.36.0-3.fc34.x86_64.rpm                       154 kB/s | 273 kB     00:01    
(5/146): colord-libs-1.4.5-2.fc34.x86_64.rpm                336 kB/s | 240 kB     00:00    
(6/146): crypto-policies-scripts-20210213-1.git5c710c0.fc34 191 kB/s |  65 kB     00:00    
(7/146): dbus-1.12.20-3.fc34.x86_64.rpm                      43 kB/s | 8.0 kB     00:00    
(8/146): dbus-common-1.12.20-3.fc34.noarch.rpm               43 kB/s |  15 kB     00:00    
(9/146): cpio-2.13-10.fc34.x86_64.rpm                       219 kB/s | 274 kB     00:01    
(10/146): desktop-file-utils-0.26-3.fc34.x86_64.rpm         897 kB/s |  74 kB     00:00    
(11/146): dbus-libs-1.12.20-3.fc34.x86_64.rpm               514 kB/s | 151 kB     00:00    
(12/146): cairo-1.17.4-3.fc34.x86_64.rpm                    301 kB/s | 671 kB     00:02    
(13/146): device-mapper-1.02.175-1.fc34.x86_64.rpm          952 kB/s | 144 kB     00:00    
(14/146): device-mapper-libs-1.02.175-1.fc34.x86_64.rpm     776 kB/s | 179 kB     00:00    
(15/146): diffutils-3.7-8.fc34.x86_64.rpm                   1.1 MB/s | 391 kB     00:00    
(16/146): flac-libs-1.3.3-7.fc34.x86_64.rpm                 876 kB/s | 220 kB     00:00    
(17/146): fribidi-1.0.10-4.fc34.x86_64.rpm                  1.0 MB/s |  86 kB     00:00    
(18/146): findutils-4.8.0-2.fc34.x86_64.rpm                 1.2 MB/s | 545 kB     00:00    
(19/146): fuse-libs-2.9.9-11.fc34.x86_64.rpm                1.0 MB/s |  99 kB     00:00    
(20/146): freetype-2.10.4-3.fc34.x86_64.rpm                 1.2 MB/s | 394 kB     00:00    
(21/146): graphite2-1.3.14-7.fc34.x86_64.rpm                771 kB/s |  95 kB     00:00    
(22/146): grubby-8.40-51.fc34.x86_64.rpm                    434 kB/s |  36 kB     00:00    
(23/146): gettext-libs-0.21-4.fc34.x86_64.rpm               1.2 MB/s | 313 kB     00:00    
(24/146): hicolor-icon-theme-0.17-10.fc34.noarch.rpm        506 kB/s |  45 kB     00:00    
(25/146): jbigkit-libs-2.1-21.fc34.x86_64.rpm               662 kB/s |  53 kB     00:00    
(26/146): gettext-0.21-4.fc34.x86_64.rpm                    1.6 MB/s | 1.1 MB     00:00    
(27/146): harfbuzz-2.7.4-3.fc34.x86_64.rpm                  1.6 MB/s | 634 kB     00:00    
(28/146): kpartx-0.8.5-4.fc34.x86_64.rpm                    527 kB/s |  49 kB     00:00    
(29/146): kbd-2.4.0-2.fc34.x86_64.rpm                       1.3 MB/s | 390 kB     00:00    
(30/146): libICE-1.0.10-6.fc34.x86_64.rpm                   789 kB/s |  71 kB     00:00    
(31/146): lcms2-2.12-1.fc34.x86_64.rpm                      1.2 MB/s | 171 kB     00:00    
(32/146): libSM-1.2.3-8.fc34.x86_64.rpm                     560 kB/s |  42 kB     00:00    
(33/146): libXau-1.0.9-6.fc34.x86_64.rpm                    379 kB/s |  31 kB     00:00    
(34/146): libXcomposite-0.4.5-5.fc34.x86_64.rpm             310 kB/s |  23 kB     00:00    
(35/146): libXcursor-1.2.0-5.fc34.x86_64.rpm                384 kB/s |  30 kB     00:00    
(36/146): libXdamage-1.1.5-5.fc34.x86_64.rpm                284 kB/s |  22 kB     00:00    
(37/146): libXext-1.3.4-6.fc34.x86_64.rpm                   391 kB/s |  39 kB     00:00    
(38/146): libXft-2.3.3-6.fc34.x86_64.rpm                    616 kB/s |  63 kB     00:00    
(39/146): kbd-misc-2.4.0-2.fc34.noarch.rpm                  2.6 MB/s | 1.5 MB     00:00    
(40/146): libXi-1.7.10-6.fc34.x86_64.rpm                    501 kB/s |  39 kB     00:00    
(41/146): libXinerama-1.1.4-8.fc34.x86_64.rpm               210 kB/s |  14 kB     00:00    
(42/146): libXrandr-1.5.2-6.fc34.x86_64.rpm                 417 kB/s |  28 kB     00:00    
(43/146): libXrender-0.9.10-14.fc34.x86_64.rpm              399 kB/s |  27 kB     00:00    
(44/146): libXtst-1.2.3-14.fc34.x86_64.rpm                  336 kB/s |  20 kB     00:00    
(45/146): libargon2-20171227-6.fc34.x86_64.rpm              428 kB/s |  29 kB     00:00    
(46/146): libasyncns-0.8-20.fc34.x86_64.rpm                 442 kB/s |  30 kB     00:00    
(47/146): libcanberra-0.30-24.fc34.x86_64.rpm               1.1 MB/s |  87 kB     00:00    
(48/146): libcanberra-gtk3-0.30-24.fc34.x86_64.rpm          441 kB/s |  32 kB     00:00    
(49/146): libcloudproviders-0.3.1-3.fc34.x86_64.rpm         528 kB/s |  46 kB     00:00    
(50/146): libdatrie-0.2.13-1.fc34.x86_64.rpm                452 kB/s |  32 kB     00:00    
(51/146): libkcapi-1.2.1-1.fc34.x86_64.rpm                  341 kB/s |  43 kB     00:00    
(52/146): libevent-2.1.12-3.fc34.x86_64.rpm                 1.7 MB/s | 268 kB     00:00    
(53/146): libjpeg-turbo-2.0.90-2.fc34.x86_64.rpm            1.0 MB/s | 176 kB     00:00    
(54/146): libkcapi-hmaccalc-1.2.1-1.fc34.x86_64.rpm         348 kB/s |  24 kB     00:00    
(55/146): libogg-1.3.4-4.fc34.x86_64.rpm                    376 kB/s |  33 kB     00:00    
(56/146): libpciaccess-0.16-4.fc34.x86_64.rpm               346 kB/s |  27 kB     00:00    
(57/146): libnl3-3.5.0-6.fc34.x86_64.rpm                    2.2 MB/s | 324 kB     00:00    
(58/146): libpng-1.6.37-10.fc34.x86_64.rpm                  1.3 MB/s | 119 kB     00:00    
(59/146): libseccomp-2.5.0-4.fc34.x86_64.rpm                817 kB/s |  71 kB     00:00    
(60/146): libtdb-1.4.3-6.fc34.x86_64.rpm                    591 kB/s |  51 kB     00:00    
(61/146): libtextstyle-0.21-4.fc34.x86_64.rpm               1.0 MB/s |  91 kB     00:00    
(62/146): libtiff-4.2.0-1.fc34.x86_64.rpm                   1.5 MB/s | 194 kB     00:00    
(63/146): libthai-0.1.28-6.fc34.x86_64.rpm                  1.4 MB/s | 213 kB     00:00    
(64/146): libtool-ltdl-2.4.6-40.fc34.x86_64.rpm             422 kB/s |  36 kB     00:00    
(65/146): libunwind-1.4.0-5.fc34.x86_64.rpm                 847 kB/s |  65 kB     00:00    
(66/146): libwayland-client-1.19.0-1.fc34.x86_64.rpm        493 kB/s |  32 kB     00:00    
(67/146): libwayland-cursor-1.19.0-1.fc34.x86_64.rpm        251 kB/s |  19 kB     00:00    
(68/146): libvorbis-1.3.7-3.fc34.x86_64.rpm                 1.4 MB/s | 199 kB     00:00    
(69/146): libwayland-egl-1.19.0-1.fc34.x86_64.rpm           161 kB/s |  12 kB     00:00    
(70/146): libwayland-server-1.19.0-1.fc34.x86_64.rpm        584 kB/s |  41 kB     00:00    
(71/146): libxshmfence-1.3-8.fc34.x86_64.rpm                122 kB/s |  12 kB     00:00    
(72/146): memstrack-0.2.2-1.fc34.x86_64.rpm                 632 kB/s |  50 kB     00:00    
(73/146): libxcb-1.13.1-7.fc34.x86_64.rpm                   1.5 MB/s | 230 kB     00:00    
(74/146): os-prober-1.77-7.fc34.x86_64.rpm                  623 kB/s |  44 kB     00:00    
(75/146): pigz-2.5-1.fc34.x86_64.rpm                        1.1 MB/s |  82 kB     00:00    
(76/146): opus-1.3.1-8.fc34.x86_64.rpm                      1.5 MB/s | 202 kB     00:00    
(77/146): qrencode-libs-4.0.2-7.fc34.x86_64.rpm             504 kB/s |  60 kB     00:00    
(78/146): pixman-0.40.0-3.fc34.x86_64.rpm                   1.7 MB/s | 274 kB     00:00    
(79/146): vulkan-loader-1.2.162.0-2.fc34.x86_64.rpm         1.0 MB/s | 126 kB     00:00    
(80/146): sound-theme-freedesktop-0.8-15.fc34.noarch.rpm    2.0 MB/s | 378 kB     00:00    
(81/146): xml-common-0.6.3-56.fc34.noarch.rpm               415 kB/s |  31 kB     00:00    
(82/146): pulseaudio-libs-14.2-3.fc34.x86_64.rpm            1.9 MB/s | 728 kB     00:00    
(83/146): xz-5.2.5-5.fc34.x86_64.rpm                        1.4 MB/s | 216 kB     00:00    
(84/146): adwaita-cursor-theme-40.1.1-1.fc34.noarch.rpm     2.0 MB/s | 625 kB     00:00    
(85/146): at-spi2-core-2.40.3-1.fc34.x86_64.rpm             1.3 MB/s | 176 kB     00:00    
(86/146): alsa-lib-1.2.5.1-2.fc34.x86_64.rpm                1.5 MB/s | 492 kB     00:00    
(87/146): avahi-libs-0.8-14.fc34.x86_64.rpm                 858 kB/s |  68 kB     00:00    
(88/146): cryptsetup-libs-2.3.6-1.fc34.x86_64.rpm           2.0 MB/s | 474 kB     00:00    
(89/146): cups-libs-2.3.3op2-7.fc34.x86_64.rpm              1.4 MB/s | 276 kB     00:00    
(90/146): dbus-broker-29-2.fc34.x86_64.rpm                  1.7 MB/s | 172 kB     00:00    
(91/146): dconf-0.40.0-3.fc34.x86_64.rpm                    1.0 MB/s | 110 kB     00:00    
(92/146): emacs-filesystem-27.2-5.fc34.noarch.rpm            94 kB/s | 8.4 kB     00:00    
(93/146): dracut-055-3.fc34.x86_64.rpm                      2.0 MB/s | 347 kB     00:00    
(94/146): file-5.39-6.fc34.x86_64.rpm                       686 kB/s |  50 kB     00:00    
(95/146): fontconfig-2.13.94-2.fc34.x86_64.rpm              1.2 MB/s | 273 kB     00:00    
(96/146): gdk-pixbuf2-2.42.6-1.fc34.x86_64.rpm              1.8 MB/s | 471 kB     00:00    
(97/146): gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64.rpm      846 kB/s |  85 kB     00:00    
(98/146): grub2-common-2.06-2.fc34.noarch.rpm               1.7 MB/s | 924 kB     00:00    
(99/146): grub2-tools-minimal-2.06-2.fc34.x86_64.rpm        2.3 MB/s | 604 kB     00:00    
(100/146): gsm-1.0.19-5.fc34.x86_64.rpm                     282 kB/s |  33 kB     00:00    
(101/146): grub2-tools-2.06-2.fc34.x86_64.rpm               1.9 MB/s | 1.8 MB     00:00    
(102/146): gtk-update-icon-cache-3.24.30-1.fc34.x86_64.rpm  295 kB/s |  35 kB     00:00    
(103/146): gstreamer1-1.19.1-2.1.18.4.fc34.x86_64.rpm       2.3 MB/s | 1.4 MB     00:00    
(104/146): adwaita-icon-theme-40.1.1-1.fc34.noarch.rpm      3.6 MB/s |  11 MB     00:02    
(105/146): iptables-legacy-libs-1.8.7-8.fc34.x86_64.rpm     467 kB/s |  40 kB     00:00    
(106/146): kmod-29-2.fc34.x86_64.rpm                        1.1 MB/s | 114 kB     00:00    
(107/146): hwdata-0.351-1.fc34.noarch.rpm                   2.9 MB/s | 1.5 MB     00:00    
(108/146): kmod-libs-29-2.fc34.x86_64.rpm                   817 kB/s |  63 kB     00:00    
(109/146): libX11-common-1.7.2-3.fc34.noarch.rpm            1.6 MB/s | 152 kB     00:00    
(110/146): libX11-1.7.2-3.fc34.x86_64.rpm                   3.1 MB/s | 646 kB     00:00    
(111/146): libX11-xcb-1.7.2-3.fc34.x86_64.rpm               144 kB/s |  11 kB     00:00    
(112/146): libXfixes-6.0.0-1.fc34.x86_64.rpm                267 kB/s |  19 kB     00:00    
(113/146): libdrm-2.4.107-1.fc34.x86_64.rpm                 2.0 MB/s | 162 kB     00:00    
(114/146): libedit-3.1-38.20210714cvs.fc34.x86_64.rpm       1.2 MB/s | 104 kB     00:00    
(115/146): libepoxy-1.5.9-1.fc34.x86_64.rpm                 2.2 MB/s | 243 kB     00:00    
(116/146): liberation-fonts-2.1.4-1.fc34.noarch.rpm         112 kB/s | 8.2 kB     00:00    
(117/146): liberation-fonts-common-2.1.4-1.fc34.noarch.rpm  182 kB/s |  15 kB     00:00    
(118/146): liberation-sans-fonts-2.1.4-1.fc34.noarch.rpm    3.8 MB/s | 607 kB     00:00    
(119/146): liberation-mono-fonts-2.1.4-1.fc34.noarch.rpm    2.3 MB/s | 501 kB     00:00    
(120/146): libgusb-0.3.7-1.fc34.x86_64.rpm                  374 kB/s |  49 kB     00:00    
(121/146): liberation-serif-fonts-2.1.4-1.fc34.noarch.rpm   3.6 MB/s | 605 kB     00:00    
(122/146): libpcap-1.10.1-1.fc34.x86_64.rpm                 1.3 MB/s | 171 kB     00:00    
(123/146): gtk3-3.24.30-1.fc34.x86_64.rpm                   2.5 MB/s | 4.8 MB     00:01    
(124/146): libibverbs-36.0-1.fc34.x86_64.rpm                1.7 MB/s | 354 kB     00:00    
(125/146): libsndfile-1.0.31-5.fc34.fc34.x86_64.rpm         2.3 MB/s | 206 kB     00:00    
(126/146): libxkbcommon-1.3.0-1.fc34.x86_64.rpm             1.6 MB/s | 144 kB     00:00    
(127/146): libwebp-1.2.1-1.fc34.x86_64.rpm                  2.5 MB/s | 279 kB     00:00    
(128/146): mesa-libgbm-21.1.7-1.fc34.x86_64.rpm             426 kB/s |  42 kB     00:00    
(129/146): nspr-4.32.0-1.fc34.x86_64.rpm                    835 kB/s | 138 kB     00:00    
(130/146): nss-3.69.0-1.fc34.x86_64.rpm                     1.3 MB/s | 684 kB     00:00    
(131/146): nss-softokn-3.69.0-1.fc34.x86_64.rpm             1.1 MB/s | 378 kB     00:00    
(132/146): nss-softokn-freebl-3.69.0-1.fc34.x86_64.rpm      1.0 MB/s | 324 kB     00:00    
(133/146): nss-sysinit-3.69.0-1.fc34.x86_64.rpm             151 kB/s |  21 kB     00:00    
(134/146): nss-util-3.69.0-1.fc34.x86_64.rpm                569 kB/s |  88 kB     00:00    
(135/146): pango-1.48.9-2.fc34.x86_64.rpm                   990 kB/s | 299 kB     00:00    
(136/146): mesa-vulkan-drivers-21.1.7-1.fc34.x86_64.rpm     2.1 MB/s | 4.8 MB     00:02    
(137/146): procps-ng-3.3.17-1.fc34.1.x86_64.rpm             1.1 MB/s | 334 kB     00:00    
(138/146): systemd-networkd-248.7-1.fc34.x86_64.rpm         1.1 MB/s | 476 kB     00:00    
(139/146): systemd-pam-248.7-1.fc34.x86_64.rpm              956 kB/s | 320 kB     00:00    
(140/146): systemd-rpm-macros-248.7-1.fc34.noarch.rpm       203 kB/s |  28 kB     00:00    
(141/146): systemd-udev-248.7-1.fc34.x86_64.rpm             1.3 MB/s | 1.5 MB     00:01    
(142/146): llvm-libs-12.0.1-1.fc34.x86_64.rpm               4.9 MB/s |  23 MB     00:04    
(143/146): which-2.21-26.fc34.x86_64.rpm                    241 kB/s |  42 kB     00:00    
(144/146): systemd-248.7-1.fc34.x86_64.rpm                  1.9 MB/s | 4.4 MB     00:02    
(145/146): xdg-utils-1.1.3-9.fc34.noarch.rpm                998 kB/s |  72 kB     00:00    
(146/146): xkeyboard-config-2.33-1.fc34.noarch.rpm          3.5 MB/s | 783 kB     00:00    
--------------------------------------------------------------------------------------------
Total                                                       4.9 MB/s |  81 MB     00:16     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                    1/1 
  Installing       : nspr-4.32.0-1.fc34.x86_64                                        1/147 
  Installing       : nss-util-3.69.0-1.fc34.x86_64                                    2/147 
  Installing       : dbus-libs-1:1.12.20-3.fc34.x86_64                                3/147 
  Installing       : libpng-2:1.6.37-10.fc34.x86_64                                   4/147 
  Installing       : atk-2.36.0-3.fc34.x86_64                                         5/147 
  Installing       : liberation-fonts-common-1:2.1.4-1.fc34.noarch                    6/147 
  Installing       : kmod-libs-29-2.fc34.x86_64                                       7/147 
  Installing       : kmod-29-2.fc34.x86_64                                            8/147 
  Installing       : libwayland-client-1.19.0-1.fc34.x86_64                           9/147 
  Installing       : libogg-2:1.3.4-4.fc34.x86_64                                    10/147 
  Installing       : libvorbis-1:1.3.7-3.fc34.x86_64                                 11/147 
  Installing       : which-2.21-26.fc34.x86_64                                       12/147 
  Installing       : libX11-xcb-1.7.2-3.fc34.x86_64                                  13/147 
  Installing       : grub2-common-1:2.06-2.fc34.noarch                               14/147 
  Installing       : alsa-lib-1.2.5.1-2.fc34.x86_64                                  15/147 
  Installing       : pixman-0.40.0-3.fc34.x86_64                                     16/147 
  Installing       : libxshmfence-1.3-8.fc34.x86_64                                  17/147 
  Installing       : libtool-ltdl-2.4.6-40.fc34.x86_64                               18/147 
  Installing       : libtextstyle-0.21-4.fc34.x86_64                                 19/147 
  Installing       : libtdb-1.4.3-6.fc34.x86_64                                      20/147 
  Installing       : libjpeg-turbo-2.0.90-2.fc34.x86_64                              21/147 
  Installing       : gdk-pixbuf2-2.42.6-1.fc34.x86_64                                22/147 
  Installing       : libICE-1.0.10-6.fc34.x86_64                                     23/147 
  Installing       : fribidi-1.0.10-4.fc34.x86_64                                    24/147 
  Installing       : findutils-1:4.8.0-2.fc34.x86_64                                 25/147 
  Installing       : libSM-1.2.3-8.fc34.x86_64                                       26/147 
  Installing       : gtk-update-icon-cache-3.24.30-1.fc34.x86_64                     27/147 
  Installing       : gettext-libs-0.21-4.fc34.x86_64                                 28/147 
  Installing       : gettext-0.21-4.fc34.x86_64                                      29/147 
  Installing       : flac-libs-1.3.3-7.fc34.x86_64                                   30/147 
  Installing       : libwayland-cursor-1.19.0-1.fc34.x86_64                          31/147 
  Installing       : liberation-mono-fonts-1:2.1.4-1.fc34.noarch                     32/147 
  Installing       : liberation-sans-fonts-1:2.1.4-1.fc34.noarch                     33/147 
  Installing       : liberation-serif-fonts-1:2.1.4-1.fc34.noarch                    34/147 
  Installing       : liberation-fonts-1:2.1.4-1.fc34.noarch                          35/147 
  Installing       : nss-softokn-freebl-3.69.0-1.fc34.x86_64                         36/147 
  Installing       : nss-softokn-3.69.0-1.fc34.x86_64                                37/147 
  Installing       : xkeyboard-config-2.33-1.fc34.noarch                             38/147 
  Installing       : libxkbcommon-1.3.0-1.fc34.x86_64                                39/147 
  Installing       : systemd-rpm-macros-248.7-1.fc34.noarch                          40/147 
  Installing       : procps-ng-3.3.17-1.fc34.1.x86_64                                41/147 
  Installing       : libwebp-1.2.1-1.fc34.x86_64                                     42/147 
  Installing       : libgusb-0.3.7-1.fc34.x86_64                                     43/147 
  Installing       : libepoxy-1.5.9-1.fc34.x86_64                                    44/147 
  Installing       : libedit-3.1-38.20210714cvs.fc34.x86_64                          45/147 
  Installing       : llvm-libs-12.0.1-1.fc34.x86_64                                  46/147 
  Installing       : libX11-common-1.7.2-3.fc34.noarch                               47/147 
  Installing       : hwdata-0.351-1.fc34.noarch                                      48/147 
  Installing       : libpciaccess-0.16-4.fc34.x86_64                                 49/147 
  Installing       : libdrm-2.4.107-1.fc34.x86_64                                    50/147 
  Installing       : gsm-1.0.19-5.fc34.x86_64                                        51/147 
  Installing       : file-5.39-6.fc34.x86_64                                         52/147 
  Installing       : emacs-filesystem-1:27.2-5.fc34.noarch                           53/147 
  Installing       : desktop-file-utils-0.26-3.fc34.x86_64                           54/147 
  Installing       : xdg-utils-1.1.3-9.fc34.noarch                                   55/147 
  Installing       : adwaita-cursor-theme-40.1.1-1.fc34.noarch                       56/147 
  Installing       : adwaita-icon-theme-40.1.1-1.fc34.noarch                         57/147 
  Installing       : xz-5.2.5-5.fc34.x86_64                                          58/147 
  Running scriptlet: xml-common-0.6.3-56.fc34.noarch                                 59/147 
  Installing       : xml-common-0.6.3-56.fc34.noarch                                 59/147 
  Installing       : sound-theme-freedesktop-0.8-15.fc34.noarch                      60/147 
  Running scriptlet: sound-theme-freedesktop-0.8-15.fc34.noarch                      60/147 
  Installing       : qrencode-libs-4.0.2-7.fc34.x86_64                               61/147 
  Installing       : pigz-2.5-1.fc34.x86_64                                          62/147 
  Installing       : opus-1.3.1-8.fc34.x86_64                                        63/147 
  Installing       : libsndfile-1.0.31-5.fc34.fc34.x86_64                            64/147 
  Installing       : memstrack-0.2.2-1.fc34.x86_64                                   65/147 
  Installing       : libwayland-server-1.19.0-1.fc34.x86_64                          66/147 
  Installing       : mesa-libgbm-21.1.7-1.fc34.x86_64                                67/147 
  Installing       : libwayland-egl-1.19.0-1.fc34.x86_64                             68/147 
  Installing       : libunwind-1.4.0-5.fc34.x86_64                                   69/147 
  Installing       : gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                          70/147 
  Installing       : libseccomp-2.5.0-4.fc34.x86_64                                  71/147 
  Installing       : libnl3-3.5.0-6.fc34.x86_64                                      72/147 
  Installing       : libibverbs-36.0-1.fc34.x86_64                                   73/147 
  Installing       : libpcap-14:1.10.1-1.fc34.x86_64                                 74/147 
  Installing       : iptables-legacy-libs-1.8.7-8.fc34.x86_64                        75/147 
  Installing       : libevent-2.1.12-3.fc34.x86_64                                   76/147 
  Installing       : avahi-libs-0.8-14.fc34.x86_64                                   77/147 
  Installing       : cups-libs-1:2.3.3op2-7.fc34.x86_64                              78/147 
  Installing       : libdatrie-0.2.13-1.fc34.x86_64                                  79/147 
  Installing       : libthai-0.1.28-6.fc34.x86_64                                    80/147 
  Installing       : libcloudproviders-0.3.1-3.fc34.x86_64                           81/147 
  Installing       : libasyncns-0.8-20.fc34.x86_64                                   82/147 
  Installing       : libargon2-20171227-6.fc34.x86_64                                83/147 
  Installing       : libXau-1.0.9-6.fc34.x86_64                                      84/147 
  Installing       : libxcb-1.13.1-7.fc34.x86_64                                     85/147 
  Installing       : libX11-1.7.2-3.fc34.x86_64                                      86/147 
  Installing       : libXext-1.3.4-6.fc34.x86_64                                     87/147 
  Installing       : libXrender-0.9.10-14.fc34.x86_64                                88/147 
  Installing       : libXfixes-6.0.0-1.fc34.x86_64                                   89/147 
  Installing       : libXi-1.7.10-6.fc34.x86_64                                      90/147 
  Installing       : libXtst-1.2.3-14.fc34.x86_64                                    91/147 
  Installing       : libXdamage-1.1.5-5.fc34.x86_64                                  92/147 
  Installing       : libXrandr-1.5.2-6.fc34.x86_64                                   93/147 
  Installing       : libXcomposite-0.4.5-5.fc34.x86_64                               94/147 
  Installing       : pulseaudio-libs-14.2-3.fc34.x86_64                              95/147 
  Installing       : libXcursor-1.2.0-5.fc34.x86_64                                  96/147 
  Installing       : libXinerama-1.1.4-8.fc34.x86_64                                 97/147 
  Installing       : vulkan-loader-1.2.162.0-2.fc34.x86_64                           98/147 
  Installing       : mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                        99/147 
  Installing       : lcms2-2.12-1.fc34.x86_64                                       100/147 
  Installing       : colord-libs-1.4.5-2.fc34.x86_64                                101/147 
  Installing       : kbd-misc-2.4.0-2.fc34.noarch                                   102/147 
  Installing       : kbd-2.4.0-2.fc34.x86_64                                        103/147 
  Installing       : jbigkit-libs-2.1-21.fc34.x86_64                                104/147 
  Installing       : libtiff-4.2.0-1.fc34.x86_64                                    105/147 
  Installing       : gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                       106/147 
  Installing       : hicolor-icon-theme-0.17-10.fc34.noarch                         107/147 
  Installing       : graphite2-1.3.14-7.fc34.x86_64                                 108/147 
  Installing       : harfbuzz-2.7.4-3.fc34.x86_64                                   109/147 
  Installing       : freetype-2.10.4-3.fc34.x86_64                                  110/147 
  Installing       : fontconfig-2.13.94-2.fc34.x86_64                               111/147 
  Running scriptlet: fontconfig-2.13.94-2.fc34.x86_64                               111/147 
  Installing       : cairo-1.17.4-3.fc34.x86_64                                     112/147 
  Installing       : cairo-gobject-1.17.4-3.fc34.x86_64                             113/147 
  Installing       : libXft-2.3.3-6.fc34.x86_64                                     114/147 
  Installing       : pango-1.48.9-2.fc34.x86_64                                     115/147 
  Installing       : fuse-libs-2.9.9-11.fc34.x86_64                                 116/147 
  Installing       : diffutils-3.7-8.fc34.x86_64                                    117/147 
  Installing       : cpio-2.13-10.fc34.x86_64                                       118/147 
  Installing       : acl-2.3.1-1.fc34.x86_64                                        119/147 
  Installing       : device-mapper-1.02.175-1.fc34.x86_64                           120/147 
  Installing       : device-mapper-libs-1.02.175-1.fc34.x86_64                      121/147 
  Installing       : cryptsetup-libs-2.3.6-1.fc34.x86_64                            122/147 
  Installing       : dbus-1:1.12.20-3.fc34.x86_64                                   123/147 
  Running scriptlet: systemd-networkd-248.7-1.fc34.x86_64                           124/147 
  Installing       : systemd-networkd-248.7-1.fc34.x86_64                           124/147 
  Running scriptlet: systemd-networkd-248.7-1.fc34.x86_64                           124/147 
  Installing       : systemd-pam-248.7-1.fc34.x86_64                                125/147 
  Running scriptlet: systemd-248.7-1.fc34.x86_64                                    126/147 
  Installing       : systemd-248.7-1.fc34.x86_64                                    126/147 
  Running scriptlet: systemd-248.7-1.fc34.x86_64                                    126/147 
  Installing       : dbus-common-1:1.12.20-3.fc34.noarch                            127/147 
  Running scriptlet: dbus-common-1:1.12.20-3.fc34.noarch                            127/147 
Created symlink /etc/systemd/system/sockets.target.wants/dbus.socket → /usr/lib/systemd/system/dbus.socket.
Created symlink /etc/systemd/user/sockets.target.wants/dbus.socket → /usr/lib/systemd/user/dbus.socket.

  Running scriptlet: dbus-broker-29-2.fc34.x86_64                                   128/147 
  Installing       : dbus-broker-29-2.fc34.x86_64                                   128/147 
  Running scriptlet: dbus-broker-29-2.fc34.x86_64                                   128/147 
Created symlink /etc/systemd/system/dbus.service → /usr/lib/systemd/system/dbus-broker.service.
Created symlink /etc/systemd/user/dbus.service → /usr/lib/systemd/user/dbus-broker.service.

  Running scriptlet: systemd-udev-248.7-1.fc34.x86_64                               129/147 
  Installing       : systemd-udev-248.7-1.fc34.x86_64                               129/147 
  Running scriptlet: systemd-udev-248.7-1.fc34.x86_64                               129/147 
  Installing       : at-spi2-core-2.40.3-1.fc34.x86_64                              130/147 
  Installing       : at-spi2-atk-2.38.0-2.fc34.x86_64                               131/147 
  Installing       : grub2-tools-minimal-1:2.06-2.fc34.x86_64                       132/147 
  Installing       : os-prober-1.77-7.fc34.x86_64                                   133/147 
  Installing       : libcanberra-0.30-24.fc34.x86_64                                134/147 
  Running scriptlet: libcanberra-0.30-24.fc34.x86_64                                134/147 
  Installing       : libkcapi-1.2.1-1.fc34.x86_64                                   135/147 
  Installing       : libkcapi-hmaccalc-1.2.1-1.fc34.x86_64                          136/147 
  Installing       : dconf-0.40.0-3.fc34.x86_64                                     137/147 
  Running scriptlet: dconf-0.40.0-3.fc34.x86_64                                     137/147 
  Installing       : libcanberra-gtk3-0.30-24.fc34.x86_64                           138/147 
  Installing       : gtk3-3.24.30-1.fc34.x86_64                                     139/147 
  Installing       : kpartx-0.8.5-4.fc34.x86_64                                     140/147 
  Installing       : dracut-055-3.fc34.x86_64                                       141/147 
  Running scriptlet: grub2-tools-1:2.06-2.fc34.x86_64                               142/147 
  Installing       : grub2-tools-1:2.06-2.fc34.x86_64                               142/147 
  Installing       : grubby-8.40-51.fc34.x86_64                                     143/147 
  Running scriptlet: grubby-8.40-51.fc34.x86_64                                     143/147 
  Installing       : crypto-policies-scripts-20210213-1.git5c710c0.fc34.noarch      144/147 
  Installing       : nss-sysinit-3.69.0-1.fc34.x86_64                               145/147 
  Installing       : nss-3.69.0-1.fc34.x86_64                                       146/147 
  Running scriptlet: nss-3.69.0-1.fc34.x86_64                                       146/147 
  Running scriptlet: google-chrome-stable-93.0.4577.63-1.x86_64                     147/147 
  Installing       : google-chrome-stable-93.0.4577.63-1.x86_64                     147/147 
  Running scriptlet: google-chrome-stable-93.0.4577.63-1.x86_64                     147/147 
  Running scriptlet: grub2-common-1:2.06-2.fc34.noarch                              147/147 
  Running scriptlet: fontconfig-2.13.94-2.fc34.x86_64                               147/147 
  Running scriptlet: dconf-0.40.0-3.fc34.x86_64                                     147/147 
  Running scriptlet: crypto-policies-scripts-20210213-1.git5c710c0.fc34.noarch      147/147 
  Running scriptlet: nss-3.69.0-1.fc34.x86_64                                       147/147 
  Running scriptlet: google-chrome-stable-93.0.4577.63-1.x86_64                     147/147 
  Verifying        : acl-2.3.1-1.fc34.x86_64                                          1/147 
  Verifying        : at-spi2-atk-2.38.0-2.fc34.x86_64                                 2/147 
  Verifying        : atk-2.36.0-3.fc34.x86_64                                         3/147 
  Verifying        : cairo-1.17.4-3.fc34.x86_64                                       4/147 
  Verifying        : cairo-gobject-1.17.4-3.fc34.x86_64                               5/147 
  Verifying        : colord-libs-1.4.5-2.fc34.x86_64                                  6/147 
  Verifying        : cpio-2.13-10.fc34.x86_64                                         7/147 
  Verifying        : crypto-policies-scripts-20210213-1.git5c710c0.fc34.noarch        8/147 
  Verifying        : dbus-1:1.12.20-3.fc34.x86_64                                     9/147 
  Verifying        : dbus-common-1:1.12.20-3.fc34.noarch                             10/147 
  Verifying        : dbus-libs-1:1.12.20-3.fc34.x86_64                               11/147 
  Verifying        : desktop-file-utils-0.26-3.fc34.x86_64                           12/147 
  Verifying        : device-mapper-1.02.175-1.fc34.x86_64                            13/147 
  Verifying        : device-mapper-libs-1.02.175-1.fc34.x86_64                       14/147 
  Verifying        : diffutils-3.7-8.fc34.x86_64                                     15/147 
  Verifying        : findutils-1:4.8.0-2.fc34.x86_64                                 16/147 
  Verifying        : flac-libs-1.3.3-7.fc34.x86_64                                   17/147 
  Verifying        : freetype-2.10.4-3.fc34.x86_64                                   18/147 
  Verifying        : fribidi-1.0.10-4.fc34.x86_64                                    19/147 
  Verifying        : fuse-libs-2.9.9-11.fc34.x86_64                                  20/147 
  Verifying        : gettext-0.21-4.fc34.x86_64                                      21/147 
  Verifying        : gettext-libs-0.21-4.fc34.x86_64                                 22/147 
  Verifying        : graphite2-1.3.14-7.fc34.x86_64                                  23/147 
  Verifying        : grubby-8.40-51.fc34.x86_64                                      24/147 
  Verifying        : harfbuzz-2.7.4-3.fc34.x86_64                                    25/147 
  Verifying        : hicolor-icon-theme-0.17-10.fc34.noarch                          26/147 
  Verifying        : jbigkit-libs-2.1-21.fc34.x86_64                                 27/147 
  Verifying        : kbd-2.4.0-2.fc34.x86_64                                         28/147 
  Verifying        : kbd-misc-2.4.0-2.fc34.noarch                                    29/147 
  Verifying        : kpartx-0.8.5-4.fc34.x86_64                                      30/147 
  Verifying        : lcms2-2.12-1.fc34.x86_64                                        31/147 
  Verifying        : libICE-1.0.10-6.fc34.x86_64                                     32/147 
  Verifying        : libSM-1.2.3-8.fc34.x86_64                                       33/147 
  Verifying        : libXau-1.0.9-6.fc34.x86_64                                      34/147 
  Verifying        : libXcomposite-0.4.5-5.fc34.x86_64                               35/147 
  Verifying        : libXcursor-1.2.0-5.fc34.x86_64                                  36/147 
  Verifying        : libXdamage-1.1.5-5.fc34.x86_64                                  37/147 
  Verifying        : libXext-1.3.4-6.fc34.x86_64                                     38/147 
  Verifying        : libXft-2.3.3-6.fc34.x86_64                                      39/147 
  Verifying        : libXi-1.7.10-6.fc34.x86_64                                      40/147 
  Verifying        : libXinerama-1.1.4-8.fc34.x86_64                                 41/147 
  Verifying        : libXrandr-1.5.2-6.fc34.x86_64                                   42/147 
  Verifying        : libXrender-0.9.10-14.fc34.x86_64                                43/147 
  Verifying        : libXtst-1.2.3-14.fc34.x86_64                                    44/147 
  Verifying        : libargon2-20171227-6.fc34.x86_64                                45/147 
  Verifying        : libasyncns-0.8-20.fc34.x86_64                                   46/147 
  Verifying        : libcanberra-0.30-24.fc34.x86_64                                 47/147 
  Verifying        : libcanberra-gtk3-0.30-24.fc34.x86_64                            48/147 
  Verifying        : libcloudproviders-0.3.1-3.fc34.x86_64                           49/147 
  Verifying        : libdatrie-0.2.13-1.fc34.x86_64                                  50/147 
  Verifying        : libevent-2.1.12-3.fc34.x86_64                                   51/147 
  Verifying        : libjpeg-turbo-2.0.90-2.fc34.x86_64                              52/147 
  Verifying        : libkcapi-1.2.1-1.fc34.x86_64                                    53/147 
  Verifying        : libkcapi-hmaccalc-1.2.1-1.fc34.x86_64                           54/147 
  Verifying        : libnl3-3.5.0-6.fc34.x86_64                                      55/147 
  Verifying        : libogg-2:1.3.4-4.fc34.x86_64                                    56/147 
  Verifying        : libpciaccess-0.16-4.fc34.x86_64                                 57/147 
  Verifying        : libpng-2:1.6.37-10.fc34.x86_64                                  58/147 
  Verifying        : libseccomp-2.5.0-4.fc34.x86_64                                  59/147 
  Verifying        : libtdb-1.4.3-6.fc34.x86_64                                      60/147 
  Verifying        : libtextstyle-0.21-4.fc34.x86_64                                 61/147 
  Verifying        : libthai-0.1.28-6.fc34.x86_64                                    62/147 
  Verifying        : libtiff-4.2.0-1.fc34.x86_64                                     63/147 
  Verifying        : libtool-ltdl-2.4.6-40.fc34.x86_64                               64/147 
  Verifying        : libunwind-1.4.0-5.fc34.x86_64                                   65/147 
  Verifying        : libvorbis-1:1.3.7-3.fc34.x86_64                                 66/147 
  Verifying        : libwayland-client-1.19.0-1.fc34.x86_64                          67/147 
  Verifying        : libwayland-cursor-1.19.0-1.fc34.x86_64                          68/147 
  Verifying        : libwayland-egl-1.19.0-1.fc34.x86_64                             69/147 
  Verifying        : libwayland-server-1.19.0-1.fc34.x86_64                          70/147 
  Verifying        : libxcb-1.13.1-7.fc34.x86_64                                     71/147 
  Verifying        : libxshmfence-1.3-8.fc34.x86_64                                  72/147 
  Verifying        : memstrack-0.2.2-1.fc34.x86_64                                   73/147 
  Verifying        : opus-1.3.1-8.fc34.x86_64                                        74/147 
  Verifying        : os-prober-1.77-7.fc34.x86_64                                    75/147 
  Verifying        : pigz-2.5-1.fc34.x86_64                                          76/147 
  Verifying        : pixman-0.40.0-3.fc34.x86_64                                     77/147 
  Verifying        : pulseaudio-libs-14.2-3.fc34.x86_64                              78/147 
  Verifying        : qrencode-libs-4.0.2-7.fc34.x86_64                               79/147 
  Verifying        : sound-theme-freedesktop-0.8-15.fc34.noarch                      80/147 
  Verifying        : vulkan-loader-1.2.162.0-2.fc34.x86_64                           81/147 
  Verifying        : xml-common-0.6.3-56.fc34.noarch                                 82/147 
  Verifying        : xz-5.2.5-5.fc34.x86_64                                          83/147 
  Verifying        : adwaita-cursor-theme-40.1.1-1.fc34.noarch                       84/147 
  Verifying        : adwaita-icon-theme-40.1.1-1.fc34.noarch                         85/147 
  Verifying        : alsa-lib-1.2.5.1-2.fc34.x86_64                                  86/147 
  Verifying        : at-spi2-core-2.40.3-1.fc34.x86_64                               87/147 
  Verifying        : avahi-libs-0.8-14.fc34.x86_64                                   88/147 
  Verifying        : cryptsetup-libs-2.3.6-1.fc34.x86_64                             89/147 
  Verifying        : cups-libs-1:2.3.3op2-7.fc34.x86_64                              90/147 
  Verifying        : dbus-broker-29-2.fc34.x86_64                                    91/147 
  Verifying        : dconf-0.40.0-3.fc34.x86_64                                      92/147 
  Verifying        : dracut-055-3.fc34.x86_64                                        93/147 
  Verifying        : emacs-filesystem-1:27.2-5.fc34.noarch                           94/147 
  Verifying        : file-5.39-6.fc34.x86_64                                         95/147 
  Verifying        : fontconfig-2.13.94-2.fc34.x86_64                                96/147 
  Verifying        : gdk-pixbuf2-2.42.6-1.fc34.x86_64                                97/147 
  Verifying        : gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                        98/147 
  Verifying        : grub2-common-1:2.06-2.fc34.noarch                               99/147 
  Verifying        : grub2-tools-1:2.06-2.fc34.x86_64                               100/147 
  Verifying        : grub2-tools-minimal-1:2.06-2.fc34.x86_64                       101/147 
  Verifying        : gsm-1.0.19-5.fc34.x86_64                                       102/147 
  Verifying        : gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                         103/147 
  Verifying        : gtk-update-icon-cache-3.24.30-1.fc34.x86_64                    104/147 
  Verifying        : gtk3-3.24.30-1.fc34.x86_64                                     105/147 
  Verifying        : hwdata-0.351-1.fc34.noarch                                     106/147 
  Verifying        : iptables-legacy-libs-1.8.7-8.fc34.x86_64                       107/147 
  Verifying        : kmod-29-2.fc34.x86_64                                          108/147 
  Verifying        : kmod-libs-29-2.fc34.x86_64                                     109/147 
  Verifying        : libX11-1.7.2-3.fc34.x86_64                                     110/147 
  Verifying        : libX11-common-1.7.2-3.fc34.noarch                              111/147 
  Verifying        : libX11-xcb-1.7.2-3.fc34.x86_64                                 112/147 
  Verifying        : libXfixes-6.0.0-1.fc34.x86_64                                  113/147 
  Verifying        : libdrm-2.4.107-1.fc34.x86_64                                   114/147 
  Verifying        : libedit-3.1-38.20210714cvs.fc34.x86_64                         115/147 
  Verifying        : libepoxy-1.5.9-1.fc34.x86_64                                   116/147 
  Verifying        : liberation-fonts-1:2.1.4-1.fc34.noarch                         117/147 
  Verifying        : liberation-fonts-common-1:2.1.4-1.fc34.noarch                  118/147 
  Verifying        : liberation-mono-fonts-1:2.1.4-1.fc34.noarch                    119/147 
  Verifying        : liberation-sans-fonts-1:2.1.4-1.fc34.noarch                    120/147 
  Verifying        : liberation-serif-fonts-1:2.1.4-1.fc34.noarch                   121/147 
  Verifying        : libgusb-0.3.7-1.fc34.x86_64                                    122/147 
  Verifying        : libibverbs-36.0-1.fc34.x86_64                                  123/147 
  Verifying        : libpcap-14:1.10.1-1.fc34.x86_64                                124/147 
  Verifying        : libsndfile-1.0.31-5.fc34.fc34.x86_64                           125/147 
  Verifying        : libwebp-1.2.1-1.fc34.x86_64                                    126/147 
  Verifying        : libxkbcommon-1.3.0-1.fc34.x86_64                               127/147 
  Verifying        : llvm-libs-12.0.1-1.fc34.x86_64                                 128/147 
  Verifying        : mesa-libgbm-21.1.7-1.fc34.x86_64                               129/147 
  Verifying        : mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                       130/147 
  Verifying        : nspr-4.32.0-1.fc34.x86_64                                      131/147 
  Verifying        : nss-3.69.0-1.fc34.x86_64                                       132/147 
  Verifying        : nss-softokn-3.69.0-1.fc34.x86_64                               133/147 
  Verifying        : nss-softokn-freebl-3.69.0-1.fc34.x86_64                        134/147 
  Verifying        : nss-sysinit-3.69.0-1.fc34.x86_64                               135/147 
  Verifying        : nss-util-3.69.0-1.fc34.x86_64                                  136/147 
  Verifying        : pango-1.48.9-2.fc34.x86_64                                     137/147 
  Verifying        : procps-ng-3.3.17-1.fc34.1.x86_64                               138/147 
  Verifying        : systemd-248.7-1.fc34.x86_64                                    139/147 
  Verifying        : systemd-networkd-248.7-1.fc34.x86_64                           140/147 
  Verifying        : systemd-pam-248.7-1.fc34.x86_64                                141/147 
  Verifying        : systemd-rpm-macros-248.7-1.fc34.noarch                         142/147 
  Verifying        : systemd-udev-248.7-1.fc34.x86_64                               143/147 
  Verifying        : which-2.21-26.fc34.x86_64                                      144/147 
  Verifying        : xdg-utils-1.1.3-9.fc34.noarch                                  145/147 
  Verifying        : xkeyboard-config-2.33-1.fc34.noarch                            146/147 
  Verifying        : google-chrome-stable-93.0.4577.63-1.x86_64                     147/147 

Installed:
  acl-2.3.1-1.fc34.x86_64                                                                   
  adwaita-cursor-theme-40.1.1-1.fc34.noarch                                                 
  adwaita-icon-theme-40.1.1-1.fc34.noarch                                                   
  alsa-lib-1.2.5.1-2.fc34.x86_64                                                            
  at-spi2-atk-2.38.0-2.fc34.x86_64                                                          
  at-spi2-core-2.40.3-1.fc34.x86_64                                                         
  atk-2.36.0-3.fc34.x86_64                                                                  
  avahi-libs-0.8-14.fc34.x86_64                                                             
  cairo-1.17.4-3.fc34.x86_64                                                                
  cairo-gobject-1.17.4-3.fc34.x86_64                                                        
  colord-libs-1.4.5-2.fc34.x86_64                                                           
  cpio-2.13-10.fc34.x86_64                                                                  
  crypto-policies-scripts-20210213-1.git5c710c0.fc34.noarch                                 
  cryptsetup-libs-2.3.6-1.fc34.x86_64                                                       
  cups-libs-1:2.3.3op2-7.fc34.x86_64                                                        
  dbus-1:1.12.20-3.fc34.x86_64                                                              
  dbus-broker-29-2.fc34.x86_64                                                              
  dbus-common-1:1.12.20-3.fc34.noarch                                                       
  dbus-libs-1:1.12.20-3.fc34.x86_64                                                         
  dconf-0.40.0-3.fc34.x86_64                                                                
  desktop-file-utils-0.26-3.fc34.x86_64                                                     
  device-mapper-1.02.175-1.fc34.x86_64                                                      
  device-mapper-libs-1.02.175-1.fc34.x86_64                                                 
  diffutils-3.7-8.fc34.x86_64                                                               
  dracut-055-3.fc34.x86_64                                                                  
  emacs-filesystem-1:27.2-5.fc34.noarch                                                     
  file-5.39-6.fc34.x86_64                                                                   
  findutils-1:4.8.0-2.fc34.x86_64                                                           
  flac-libs-1.3.3-7.fc34.x86_64                                                             
  fontconfig-2.13.94-2.fc34.x86_64                                                          
  freetype-2.10.4-3.fc34.x86_64                                                             
  fribidi-1.0.10-4.fc34.x86_64                                                              
  fuse-libs-2.9.9-11.fc34.x86_64                                                            
  gdk-pixbuf2-2.42.6-1.fc34.x86_64                                                          
  gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                                                  
  gettext-0.21-4.fc34.x86_64                                                                
  gettext-libs-0.21-4.fc34.x86_64                                                           
  google-chrome-stable-93.0.4577.63-1.x86_64                                                
  graphite2-1.3.14-7.fc34.x86_64                                                            
  grub2-common-1:2.06-2.fc34.noarch                                                         
  grub2-tools-1:2.06-2.fc34.x86_64                                                          
  grub2-tools-minimal-1:2.06-2.fc34.x86_64                                                  
  grubby-8.40-51.fc34.x86_64                                                                
  gsm-1.0.19-5.fc34.x86_64                                                                  
  gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                                                    
  gtk-update-icon-cache-3.24.30-1.fc34.x86_64                                               
  gtk3-3.24.30-1.fc34.x86_64                                                                
  harfbuzz-2.7.4-3.fc34.x86_64                                                              
  hicolor-icon-theme-0.17-10.fc34.noarch                                                    
  hwdata-0.351-1.fc34.noarch                                                                
  iptables-legacy-libs-1.8.7-8.fc34.x86_64                                                  
  jbigkit-libs-2.1-21.fc34.x86_64                                                           
  kbd-2.4.0-2.fc34.x86_64                                                                   
  kbd-misc-2.4.0-2.fc34.noarch                                                              
  kmod-29-2.fc34.x86_64                                                                     
  kmod-libs-29-2.fc34.x86_64                                                                
  kpartx-0.8.5-4.fc34.x86_64                                                                
  lcms2-2.12-1.fc34.x86_64                                                                  
  libICE-1.0.10-6.fc34.x86_64                                                               
  libSM-1.2.3-8.fc34.x86_64                                                                 
  libX11-1.7.2-3.fc34.x86_64                                                                
  libX11-common-1.7.2-3.fc34.noarch                                                         
  libX11-xcb-1.7.2-3.fc34.x86_64                                                            
  libXau-1.0.9-6.fc34.x86_64                                                                
  libXcomposite-0.4.5-5.fc34.x86_64                                                         
  libXcursor-1.2.0-5.fc34.x86_64                                                            
  libXdamage-1.1.5-5.fc34.x86_64                                                            
  libXext-1.3.4-6.fc34.x86_64                                                               
  libXfixes-6.0.0-1.fc34.x86_64                                                             
  libXft-2.3.3-6.fc34.x86_64                                                                
  libXi-1.7.10-6.fc34.x86_64                                                                
  libXinerama-1.1.4-8.fc34.x86_64                                                           
  libXrandr-1.5.2-6.fc34.x86_64                                                             
  libXrender-0.9.10-14.fc34.x86_64                                                          
  libXtst-1.2.3-14.fc34.x86_64                                                              
  libargon2-20171227-6.fc34.x86_64                                                          
  libasyncns-0.8-20.fc34.x86_64                                                             
  libcanberra-0.30-24.fc34.x86_64                                                           
  libcanberra-gtk3-0.30-24.fc34.x86_64                                                      
  libcloudproviders-0.3.1-3.fc34.x86_64                                                     
  libdatrie-0.2.13-1.fc34.x86_64                                                            
  libdrm-2.4.107-1.fc34.x86_64                                                              
  libedit-3.1-38.20210714cvs.fc34.x86_64                                                    
  libepoxy-1.5.9-1.fc34.x86_64                                                              
  liberation-fonts-1:2.1.4-1.fc34.noarch                                                    
  liberation-fonts-common-1:2.1.4-1.fc34.noarch                                             
  liberation-mono-fonts-1:2.1.4-1.fc34.noarch                                               
  liberation-sans-fonts-1:2.1.4-1.fc34.noarch                                               
  liberation-serif-fonts-1:2.1.4-1.fc34.noarch                                              
  libevent-2.1.12-3.fc34.x86_64                                                             
  libgusb-0.3.7-1.fc34.x86_64                                                               
  libibverbs-36.0-1.fc34.x86_64                                                             
  libjpeg-turbo-2.0.90-2.fc34.x86_64                                                        
  libkcapi-1.2.1-1.fc34.x86_64                                                              
  libkcapi-hmaccalc-1.2.1-1.fc34.x86_64                                                     
  libnl3-3.5.0-6.fc34.x86_64                                                                
  libogg-2:1.3.4-4.fc34.x86_64                                                              
  libpcap-14:1.10.1-1.fc34.x86_64                                                           
  libpciaccess-0.16-4.fc34.x86_64                                                           
  libpng-2:1.6.37-10.fc34.x86_64                                                            
  libseccomp-2.5.0-4.fc34.x86_64                                                            
  libsndfile-1.0.31-5.fc34.fc34.x86_64                                                      
  libtdb-1.4.3-6.fc34.x86_64                                                                
  libtextstyle-0.21-4.fc34.x86_64                                                           
  libthai-0.1.28-6.fc34.x86_64                                                              
  libtiff-4.2.0-1.fc34.x86_64                                                               
  libtool-ltdl-2.4.6-40.fc34.x86_64                                                         
  libunwind-1.4.0-5.fc34.x86_64                                                             
  libvorbis-1:1.3.7-3.fc34.x86_64                                                           
  libwayland-client-1.19.0-1.fc34.x86_64                                                    
  libwayland-cursor-1.19.0-1.fc34.x86_64                                                    
  libwayland-egl-1.19.0-1.fc34.x86_64                                                       
  libwayland-server-1.19.0-1.fc34.x86_64                                                    
  libwebp-1.2.1-1.fc34.x86_64                                                               
  libxcb-1.13.1-7.fc34.x86_64                                                               
  libxkbcommon-1.3.0-1.fc34.x86_64                                                          
  libxshmfence-1.3-8.fc34.x86_64                                                            
  llvm-libs-12.0.1-1.fc34.x86_64                                                            
  memstrack-0.2.2-1.fc34.x86_64                                                             
  mesa-libgbm-21.1.7-1.fc34.x86_64                                                          
  mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                                                  
  nspr-4.32.0-1.fc34.x86_64                                                                 
  nss-3.69.0-1.fc34.x86_64                                                                  
  nss-softokn-3.69.0-1.fc34.x86_64                                                          
  nss-softokn-freebl-3.69.0-1.fc34.x86_64                                                   
  nss-sysinit-3.69.0-1.fc34.x86_64                                                          
  nss-util-3.69.0-1.fc34.x86_64                                                             
  opus-1.3.1-8.fc34.x86_64                                                                  
  os-prober-1.77-7.fc34.x86_64                                                              
  pango-1.48.9-2.fc34.x86_64                                                                
  pigz-2.5-1.fc34.x86_64                                                                    
  pixman-0.40.0-3.fc34.x86_64                                                               
  procps-ng-3.3.17-1.fc34.1.x86_64                                                          
  pulseaudio-libs-14.2-3.fc34.x86_64                                                        
  qrencode-libs-4.0.2-7.fc34.x86_64                                                         
  sound-theme-freedesktop-0.8-15.fc34.noarch                                                
  systemd-248.7-1.fc34.x86_64                                                               
  systemd-networkd-248.7-1.fc34.x86_64                                                      
  systemd-pam-248.7-1.fc34.x86_64                                                           
  systemd-rpm-macros-248.7-1.fc34.noarch                                                    
  systemd-udev-248.7-1.fc34.x86_64                                                          
  vulkan-loader-1.2.162.0-2.fc34.x86_64                                                     
  which-2.21-26.fc34.x86_64                                                                 
  xdg-utils-1.1.3-9.fc34.noarch                                                             
  xkeyboard-config-2.33-1.fc34.noarch                                                       
  xml-common-0.6.3-56.fc34.noarch                                                           
  xz-5.2.5-5.fc34.x86_64                                                                    

Complete!
```

## Remove an RPM package, document the process

```bash
# In this example we will the opposite from above, the previous used command
# was "install", so in this case is "remove"

# We will remove the same RMP package mentioned above, google chrome.
# google-chrome-stable_current_x86_64.rpm

[root@c80ced9a3596 /]# sudo dnf remove google-chrome-stable-93.0.4577.63-1.x86_64
Dependencies resolved.
============================================================================================
 Package                     Arch       Version                     Repository         Size
============================================================================================
Removing:
 google-chrome-stable        x86_64     93.0.4577.63-1              @@commandline     248 M
Removing unused dependencies:
 adwaita-cursor-theme        noarch     40.1.1-1.fc34               @updates           12 M
 adwaita-icon-theme          noarch     40.1.1-1.fc34               @updates           11 M
 alsa-lib                    x86_64     1.2.5.1-2.fc34              @updates          1.4 M
 at-spi2-atk                 x86_64     2.38.0-2.fc34               @fedora           272 k
 at-spi2-core                x86_64     2.40.3-1.fc34               @updates          516 k
 atk                         x86_64     2.36.0-3.fc34               @fedora           1.2 M
 avahi-libs                  x86_64     0.8-14.fc34                 @updates          180 k
 cairo                       x86_64     1.17.4-3.fc34               @fedora           1.6 M
 cairo-gobject               x86_64     1.17.4-3.fc34               @fedora            43 k
 colord-libs                 x86_64     1.4.5-2.fc34                @fedora           857 k
 cups-libs                   x86_64     1:2.3.3op2-7.fc34           @updates          690 k
 dbus-libs                   x86_64     1:1.12.20-3.fc34            @fedora           357 k
 dconf                       x86_64     0.40.0-3.fc34               @updates          305 k
 desktop-file-utils          x86_64     0.26-3.fc34                 @fedora           251 k
 emacs-filesystem            noarch     1:27.2-5.fc34               @updates            0  
 flac-libs                   x86_64     1.3.3-7.fc34                @fedora           556 k
 fontconfig                  x86_64     2.13.94-2.fc34              @updates          821 k
 freetype                    x86_64     2.10.4-3.fc34               @fedora           821 k
 fribidi                     x86_64     1.0.10-4.fc34               @fedora           339 k
 gdk-pixbuf2                 x86_64     2.42.6-1.fc34               @updates          2.5 M
 gdk-pixbuf2-modules         x86_64     2.42.6-1.fc34               @updates          267 k
 graphite2                   x86_64     1.3.14-7.fc34               @fedora           197 k
 gsm                         x86_64     1.0.19-5.fc34               @updates           64 k
 gstreamer1                  x86_64     1.19.1-2.1.18.4.fc34        @updates          4.7 M
 gtk-update-icon-cache       x86_64     3.24.30-1.fc34              @updates           67 k
 gtk3                        x86_64     3.24.30-1.fc34              @updates           19 M
 harfbuzz                    x86_64     2.7.4-3.fc34                @fedora           1.6 M
 hicolor-icon-theme          noarch     0.17-10.fc34                @fedora            72 k
 hwdata                      noarch     0.351-1.fc34                @updates          8.2 M
 jbigkit-libs                x86_64     2.1-21.fc34                 @fedora           114 k
 lcms2                       x86_64     2.12-1.fc34                 @fedora           403 k
 libICE                      x86_64     1.0.10-6.fc34               @fedora           171 k
 libSM                       x86_64     1.2.3-8.fc34                @fedora            93 k
 libX11                      x86_64     1.7.2-3.fc34                @updates          1.3 M
 libX11-common               noarch     1.7.2-3.fc34                @updates          1.3 M
 libX11-xcb                  x86_64     1.7.2-3.fc34                @updates           15 k
 libXau                      x86_64     1.0.9-6.fc34                @fedora            64 k
 libXcomposite               x86_64     0.4.5-5.fc34                @fedora            42 k
 libXcursor                  x86_64     1.2.0-5.fc34                @fedora            50 k
 libXdamage                  x86_64     1.1.5-5.fc34                @fedora            36 k
 libXext                     x86_64     1.3.4-6.fc34                @fedora            94 k
 libXfixes                   x86_64     6.0.0-1.fc34                @updates           34 k
 libXft                      x86_64     2.3.3-6.fc34                @fedora           133 k
 libXi                       x86_64     1.7.10-6.fc34               @fedora            73 k
 libXinerama                 x86_64     1.1.4-8.fc34                @fedora            19 k
 libXrandr                   x86_64     1.5.2-6.fc34                @fedora            52 k
 libXrender                  x86_64     0.9.10-14.fc34              @fedora            50 k
 libXtst                     x86_64     1.2.3-14.fc34               @fedora            38 k
 libasyncns                  x86_64     0.8-20.fc34                 @fedora            59 k
 libcanberra                 x86_64     0.30-24.fc34                @fedora           283 k
 libcanberra-gtk3            x86_64     0.30-24.fc34                @fedora            75 k
 libcloudproviders           x86_64     0.3.1-3.fc34                @fedora           124 k
 libdatrie                   x86_64     0.2.13-1.fc34               @fedora            58 k
 libdrm                      x86_64     2.4.107-1.fc34              @updates          417 k
 libedit                     x86_64     3.1-38.20210714cvs.fc34     @updates          247 k
 libepoxy                    x86_64     1.5.9-1.fc34                @updates          1.2 M
 liberation-fonts            noarch     1:2.1.4-1.fc34              @updates            0  
 liberation-fonts-common     noarch     1:2.1.4-1.fc34              @updates           12 k
 liberation-mono-fonts       noarch     1:2.1.4-1.fc34              @updates          1.1 M
 liberation-sans-fonts       noarch     1:2.1.4-1.fc34              @updates          1.6 M
 liberation-serif-fonts      noarch     1:2.1.4-1.fc34              @updates          1.5 M
 libevent                    x86_64     2.1.12-3.fc34               @fedora           912 k
 libgusb                     x86_64     0.3.7-1.fc34                @updates          125 k
 libjpeg-turbo               x86_64     2.0.90-2.fc34               @fedora           601 k
 libogg                      x86_64     2:1.3.4-4.fc34              @fedora            49 k
 libpciaccess                x86_64     0.16-4.fc34                 @fedora            49 k
 libpng                      x86_64     2:1.6.37-10.fc34            @fedora           234 k
 libsndfile                  x86_64     1.0.31-5.fc34.fc34          @updates          522 k
 libtdb                      x86_64     1.4.3-6.fc34                @fedora           101 k
 libthai                     x86_64     0.1.28-6.fc34               @fedora           760 k
 libtiff                     x86_64     4.2.0-1.fc34                @fedora           560 k
 libtool-ltdl                x86_64     2.4.6-40.fc34               @fedora            71 k
 libunwind                   x86_64     1.4.0-5.fc34                @fedora           165 k
 libvorbis                   x86_64     1:1.3.7-3.fc34              @fedora           907 k
 libwayland-client           x86_64     1.19.0-1.fc34               @fedora            66 k
 libwayland-cursor           x86_64     1.19.0-1.fc34               @fedora            37 k
 libwayland-egl              x86_64     1.19.0-1.fc34               @fedora            17 k
 libwayland-server           x86_64     1.19.0-1.fc34               @fedora            87 k
 libwebp                     x86_64     1.2.1-1.fc34                @updates          785 k
 libxcb                      x86_64     1.13.1-7.fc34               @fedora           1.1 M
 libxshmfence                x86_64     1.3-8.fc34                  @fedora            16 k
 llvm-libs                   x86_64     12.0.1-1.fc34               @updates           92 M
 mesa-libgbm                 x86_64     21.1.7-1.fc34               @updates           65 k
 mesa-vulkan-drivers         x86_64     21.1.7-1.fc34               @updates           25 M
 nspr                        x86_64     4.32.0-1.fc34               @updates          321 k
 nss                         x86_64     3.69.0-1.fc34               @updates          2.0 M
 nss-softokn                 x86_64     3.69.0-1.fc34               @updates          1.7 M
 nss-softokn-freebl          x86_64     3.69.0-1.fc34               @updates          749 k
 nss-sysinit                 x86_64     3.69.0-1.fc34               @updates           19 k
 nss-util                    x86_64     3.69.0-1.fc34               @updates          221 k
 opus                        x86_64     1.3.1-8.fc34                @fedora           359 k
 pango                       x86_64     1.48.9-2.fc34               @updates          880 k
 pixman                      x86_64     0.40.0-3.fc34               @fedora           695 k
 pulseaudio-libs             x86_64     14.2-3.fc34                 @fedora           3.6 M
 sound-theme-freedesktop     noarch     0.8-15.fc34                 @fedora           460 k
 vulkan-loader               x86_64     1.2.162.0-2.fc34            @fedora           380 k
 xdg-utils                   noarch     1.1.3-9.fc34                @updates          313 k
 xml-common                  noarch     0.6.3-56.fc34               @fedora            78 k

Transaction Summary
============================================================================================
Remove  99 Packages

Freed space: 464 M
Is this ok [y/N]: y
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                    1/1 
  Running scriptlet: google-chrome-stable-93.0.4577.63-1.x86_64                        1/99 
  Erasing          : google-chrome-stable-93.0.4577.63-1.x86_64                        1/99 
  Running scriptlet: google-chrome-stable-93.0.4577.63-1.x86_64                        1/99 
  Erasing          : gtk3-3.24.30-1.fc34.x86_64                                        2/99 
  Erasing          : nss-3.69.0-1.fc34.x86_64                                          3/99 
  Erasing          : nss-softokn-3.69.0-1.fc34.x86_64                                  4/99 
  Erasing          : libcanberra-gtk3-0.30-24.fc34.x86_64                              5/99 
  Erasing          : pango-1.48.9-2.fc34.x86_64                                        6/99 
  Erasing          : mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                          7/99 
  Erasing          : liberation-fonts-1:2.1.4-1.fc34.noarch                            8/99 
  Erasing          : liberation-mono-fonts-1:2.1.4-1.fc34.noarch                       9/99 
  Erasing          : liberation-sans-fonts-1:2.1.4-1.fc34.noarch                      10/99 
  Erasing          : liberation-serif-fonts-1:2.1.4-1.fc34.noarch                     11/99 
  Erasing          : adwaita-icon-theme-40.1.1-1.fc34.noarch                          12/99 
  Erasing          : xdg-utils-1.1.3-9.fc34.noarch                                    13/99 
  Erasing          : cairo-gobject-1.17.4-3.fc34.x86_64                               14/99 
  Running scriptlet: libcanberra-0.30-24.fc34.x86_64                                  15/99 
System has not been booted with systemd as init system (PID 1). Can't operate.
Failed to connect to bus: Host is down

  Erasing          : libcanberra-0.30-24.fc34.x86_64                                  15/99 
  Erasing          : pulseaudio-libs-14.2-3.fc34.x86_64                               16/99 
  Erasing          : cairo-1.17.4-3.fc34.x86_64                                       17/99 
  Erasing          : libsndfile-1.0.31-5.fc34.fc34.x86_64                             18/99 
  Erasing          : nss-sysinit-3.69.0-1.fc34.x86_64                                 19/99 
  Erasing          : at-spi2-atk-2.38.0-2.fc34.x86_64                                 20/99 
  Erasing          : at-spi2-core-2.40.3-1.fc34.x86_64                                21/99 
  Erasing          : libXft-2.3.3-6.fc34.x86_64                                       22/99 
  Erasing          : fontconfig-2.13.94-2.fc34.x86_64                                 23/99 
  Running scriptlet: fontconfig-2.13.94-2.fc34.x86_64                                 23/99 
  Erasing          : libXtst-1.2.3-14.fc34.x86_64                                     24/99 
  Erasing          : gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                         25/99 
  Erasing          : libtiff-4.2.0-1.fc34.x86_64                                      26/99 
  Erasing          : libXcursor-1.2.0-5.fc34.x86_64                                   27/99 
  Erasing          : libXrandr-1.5.2-6.fc34.x86_64                                    28/99 
  Erasing          : colord-libs-1.4.5-2.fc34.x86_64                                  29/99 
  Erasing          : libXi-1.7.10-6.fc34.x86_64                                       30/99 
  Erasing          : harfbuzz-2.7.4-3.fc34.x86_64                                     31/99 
  Erasing          : freetype-2.10.4-3.fc34.x86_64                                    32/99 
  Erasing          : libXinerama-1.1.4-8.fc34.x86_64                                  33/99 
  Erasing          : libXext-1.3.4-6.fc34.x86_64                                      34/99 
  Erasing          : libXrender-0.9.10-14.fc34.x86_64                                 35/99 
  Erasing          : libthai-0.1.28-6.fc34.x86_64                                     36/99 
  Erasing          : nss-softokn-freebl-3.69.0-1.fc34.x86_64                          37/99 
  Erasing          : nss-util-3.69.0-1.fc34.x86_64                                    38/99 
  Erasing          : libXdamage-1.1.5-5.fc34.x86_64                                   39/99 
  Erasing          : libXfixes-6.0.0-1.fc34.x86_64                                    40/99 
  Erasing          : cups-libs-1:2.3.3op2-7.fc34.x86_64                               41/99 
  Erasing          : avahi-libs-0.8-14.fc34.x86_64                                    42/99 
  Erasing          : mesa-libgbm-21.1.7-1.fc34.x86_64                                 43/99 
  Erasing          : libdrm-2.4.107-1.fc34.x86_64                                     44/99 
  Erasing          : libpciaccess-0.16-4.fc34.x86_64                                  45/99 
  Erasing          : flac-libs-1.3.3-7.fc34.x86_64                                    46/99 
  Erasing          : libvorbis-1:1.3.7-3.fc34.x86_64                                  47/99 
  Erasing          : libSM-1.2.3-8.fc34.x86_64                                        48/99 
  Erasing          : gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                           49/99 
  Erasing          : desktop-file-utils-0.26-3.fc34.x86_64                            50/99 
  Erasing          : llvm-libs-12.0.1-1.fc34.x86_64                                   51/99 
  Erasing          : gtk-update-icon-cache-3.24.30-1.fc34.x86_64                      52/99 
  Erasing          : gdk-pixbuf2-2.42.6-1.fc34.x86_64                                 53/99 
  Erasing          : libXcomposite-0.4.5-5.fc34.x86_64                                54/99 
  Erasing          : libX11-1.7.2-3.fc34.x86_64                                       55/99 
  Erasing          : libxcb-1.13.1-7.fc34.x86_64                                      56/99 
  Erasing          : libwayland-cursor-1.19.0-1.fc34.x86_64                           57/99 
  Erasing          : libX11-common-1.7.2-3.fc34.noarch                                58/99 
  Erasing          : emacs-filesystem-1:27.2-5.fc34.noarch                            59/99 
  Erasing          : hwdata-0.351-1.fc34.noarch                                       60/99 
  Erasing          : xml-common-0.6.3-56.fc34.noarch                                  61/99 
warning: /etc/xml/catalog saved as /etc/xml/catalog.rpmsave

  Erasing          : sound-theme-freedesktop-0.8-15.fc34.noarch                       62/99 
  Running scriptlet: sound-theme-freedesktop-0.8-15.fc34.noarch                       62/99 
  Erasing          : adwaita-cursor-theme-40.1.1-1.fc34.noarch                        63/99 
  Erasing          : liberation-fonts-common-1:2.1.4-1.fc34.noarch                    64/99 
  Erasing          : hicolor-icon-theme-0.17-10.fc34.noarch                           65/99 
  Erasing          : libwayland-client-1.19.0-1.fc34.x86_64                           66/99 
  Erasing          : libXau-1.0.9-6.fc34.x86_64                                       67/99 
  Erasing          : libjpeg-turbo-2.0.90-2.fc34.x86_64                               68/99 
  Erasing          : libpng-2:1.6.37-10.fc34.x86_64                                   69/99 
  Erasing          : libedit-3.1-38.20210714cvs.fc34.x86_64                           70/99 
  Erasing          : libunwind-1.4.0-5.fc34.x86_64                                    71/99 
  Erasing          : libICE-1.0.10-6.fc34.x86_64                                      72/99 
  Erasing          : libogg-2:1.3.4-4.fc34.x86_64                                     73/99 
  Erasing          : libwayland-server-1.19.0-1.fc34.x86_64                           74/99 
  Erasing          : dbus-libs-1:1.12.20-3.fc34.x86_64                                75/99 
  Erasing          : libevent-2.1.12-3.fc34.x86_64                                    76/99 
  Erasing          : nspr-4.32.0-1.fc34.x86_64                                        77/99 
  Erasing          : libdatrie-0.2.13-1.fc34.x86_64                                   78/99 
  Erasing          : graphite2-1.3.14-7.fc34.x86_64                                   79/99 
  Erasing          : libgusb-0.3.7-1.fc34.x86_64                                      80/99 
  Erasing          : lcms2-2.12-1.fc34.x86_64                                         81/99 
  Erasing          : jbigkit-libs-2.1-21.fc34.x86_64                                  82/99 
  Erasing          : libwebp-1.2.1-1.fc34.x86_64                                      83/99 
  Erasing          : atk-2.36.0-3.fc34.x86_64                                         84/99 
  Erasing          : gsm-1.0.19-5.fc34.x86_64                                         85/99 
  Erasing          : opus-1.3.1-8.fc34.x86_64                                         86/99 
  Erasing          : pixman-0.40.0-3.fc34.x86_64                                      87/99 
  Erasing          : libX11-xcb-1.7.2-3.fc34.x86_64                                   88/99 
  Erasing          : libasyncns-0.8-20.fc34.x86_64                                    89/99 
  Erasing          : alsa-lib-1.2.5.1-2.fc34.x86_64                                   90/99 
  Erasing          : libtool-ltdl-2.4.6-40.fc34.x86_64                                91/99 
  Erasing          : libtdb-1.4.3-6.fc34.x86_64                                       92/99 
  Erasing          : libxshmfence-1.3-8.fc34.x86_64                                   93/99 
  Erasing          : vulkan-loader-1.2.162.0-2.fc34.x86_64                            94/99 
  Erasing          : fribidi-1.0.10-4.fc34.x86_64                                     95/99 
  Erasing          : libcloudproviders-0.3.1-3.fc34.x86_64                            96/99 
  Erasing          : libepoxy-1.5.9-1.fc34.x86_64                                     97/99 
  Erasing          : libwayland-egl-1.19.0-1.fc34.x86_64                              98/99 
  Running scriptlet: dconf-0.40.0-3.fc34.x86_64                                       99/99 
  Erasing          : dconf-0.40.0-3.fc34.x86_64                                       99/99 
  Running scriptlet: dconf-0.40.0-3.fc34.x86_64                                       99/99 
  Verifying        : adwaita-cursor-theme-40.1.1-1.fc34.noarch                         1/99 
  Verifying        : adwaita-icon-theme-40.1.1-1.fc34.noarch                           2/99 
  Verifying        : alsa-lib-1.2.5.1-2.fc34.x86_64                                    3/99 
  Verifying        : at-spi2-atk-2.38.0-2.fc34.x86_64                                  4/99 
  Verifying        : at-spi2-core-2.40.3-1.fc34.x86_64                                 5/99 
  Verifying        : atk-2.36.0-3.fc34.x86_64                                          6/99 
  Verifying        : avahi-libs-0.8-14.fc34.x86_64                                     7/99 
  Verifying        : cairo-1.17.4-3.fc34.x86_64                                        8/99 
  Verifying        : cairo-gobject-1.17.4-3.fc34.x86_64                                9/99 
  Verifying        : colord-libs-1.4.5-2.fc34.x86_64                                  10/99 
  Verifying        : cups-libs-1:2.3.3op2-7.fc34.x86_64                               11/99 
  Verifying        : dbus-libs-1:1.12.20-3.fc34.x86_64                                12/99 
  Verifying        : dconf-0.40.0-3.fc34.x86_64                                       13/99 
  Verifying        : desktop-file-utils-0.26-3.fc34.x86_64                            14/99 
  Verifying        : emacs-filesystem-1:27.2-5.fc34.noarch                            15/99 
  Verifying        : flac-libs-1.3.3-7.fc34.x86_64                                    16/99 
  Verifying        : fontconfig-2.13.94-2.fc34.x86_64                                 17/99 
  Verifying        : freetype-2.10.4-3.fc34.x86_64                                    18/99 
  Verifying        : fribidi-1.0.10-4.fc34.x86_64                                     19/99 
  Verifying        : gdk-pixbuf2-2.42.6-1.fc34.x86_64                                 20/99 
  Verifying        : gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                         21/99 
  Verifying        : google-chrome-stable-93.0.4577.63-1.x86_64                       22/99 
  Verifying        : graphite2-1.3.14-7.fc34.x86_64                                   23/99 
  Verifying        : gsm-1.0.19-5.fc34.x86_64                                         24/99 
  Verifying        : gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                           25/99 
  Verifying        : gtk-update-icon-cache-3.24.30-1.fc34.x86_64                      26/99 
  Verifying        : gtk3-3.24.30-1.fc34.x86_64                                       27/99 
  Verifying        : harfbuzz-2.7.4-3.fc34.x86_64                                     28/99 
  Verifying        : hicolor-icon-theme-0.17-10.fc34.noarch                           29/99 
  Verifying        : hwdata-0.351-1.fc34.noarch                                       30/99 
  Verifying        : jbigkit-libs-2.1-21.fc34.x86_64                                  31/99 
  Verifying        : lcms2-2.12-1.fc34.x86_64                                         32/99 
  Verifying        : libICE-1.0.10-6.fc34.x86_64                                      33/99 
  Verifying        : libSM-1.2.3-8.fc34.x86_64                                        34/99 
  Verifying        : libX11-1.7.2-3.fc34.x86_64                                       35/99 
  Verifying        : libX11-common-1.7.2-3.fc34.noarch                                36/99 
  Verifying        : libX11-xcb-1.7.2-3.fc34.x86_64                                   37/99 
  Verifying        : libXau-1.0.9-6.fc34.x86_64                                       38/99 
  Verifying        : libXcomposite-0.4.5-5.fc34.x86_64                                39/99 
  Verifying        : libXcursor-1.2.0-5.fc34.x86_64                                   40/99 
  Verifying        : libXdamage-1.1.5-5.fc34.x86_64                                   41/99 
  Verifying        : libXext-1.3.4-6.fc34.x86_64                                      42/99 
  Verifying        : libXfixes-6.0.0-1.fc34.x86_64                                    43/99 
  Verifying        : libXft-2.3.3-6.fc34.x86_64                                       44/99 
  Verifying        : libXi-1.7.10-6.fc34.x86_64                                       45/99 
  Verifying        : libXinerama-1.1.4-8.fc34.x86_64                                  46/99 
  Verifying        : libXrandr-1.5.2-6.fc34.x86_64                                    47/99 
  Verifying        : libXrender-0.9.10-14.fc34.x86_64                                 48/99 
  Verifying        : libXtst-1.2.3-14.fc34.x86_64                                     49/99 
  Verifying        : libasyncns-0.8-20.fc34.x86_64                                    50/99 
  Verifying        : libcanberra-0.30-24.fc34.x86_64                                  51/99 
  Verifying        : libcanberra-gtk3-0.30-24.fc34.x86_64                             52/99 
  Verifying        : libcloudproviders-0.3.1-3.fc34.x86_64                            53/99 
  Verifying        : libdatrie-0.2.13-1.fc34.x86_64                                   54/99 
  Verifying        : libdrm-2.4.107-1.fc34.x86_64                                     55/99 
  Verifying        : libedit-3.1-38.20210714cvs.fc34.x86_64                           56/99 
  Verifying        : libepoxy-1.5.9-1.fc34.x86_64                                     57/99 
  Verifying        : liberation-fonts-1:2.1.4-1.fc34.noarch                           58/99 
  Verifying        : liberation-fonts-common-1:2.1.4-1.fc34.noarch                    59/99 
  Verifying        : liberation-mono-fonts-1:2.1.4-1.fc34.noarch                      60/99 
  Verifying        : liberation-sans-fonts-1:2.1.4-1.fc34.noarch                      61/99 
  Verifying        : liberation-serif-fonts-1:2.1.4-1.fc34.noarch                     62/99 
  Verifying        : libevent-2.1.12-3.fc34.x86_64                                    63/99 
  Verifying        : libgusb-0.3.7-1.fc34.x86_64                                      64/99 
  Verifying        : libjpeg-turbo-2.0.90-2.fc34.x86_64                               65/99 
  Verifying        : libogg-2:1.3.4-4.fc34.x86_64                                     66/99 
  Verifying        : libpciaccess-0.16-4.fc34.x86_64                                  67/99 
  Verifying        : libpng-2:1.6.37-10.fc34.x86_64                                   68/99 
  Verifying        : libsndfile-1.0.31-5.fc34.fc34.x86_64                             69/99 
  Verifying        : libtdb-1.4.3-6.fc34.x86_64                                       70/99 
  Verifying        : libthai-0.1.28-6.fc34.x86_64                                     71/99 
  Verifying        : libtiff-4.2.0-1.fc34.x86_64                                      72/99 
  Verifying        : libtool-ltdl-2.4.6-40.fc34.x86_64                                73/99 
  Verifying        : libunwind-1.4.0-5.fc34.x86_64                                    74/99 
  Verifying        : libvorbis-1:1.3.7-3.fc34.x86_64                                  75/99 
  Verifying        : libwayland-client-1.19.0-1.fc34.x86_64                           76/99 
  Verifying        : libwayland-cursor-1.19.0-1.fc34.x86_64                           77/99 
  Verifying        : libwayland-egl-1.19.0-1.fc34.x86_64                              78/99 
  Verifying        : libwayland-server-1.19.0-1.fc34.x86_64                           79/99 
  Verifying        : libwebp-1.2.1-1.fc34.x86_64                                      80/99 
  Verifying        : libxcb-1.13.1-7.fc34.x86_64                                      81/99 
  Verifying        : libxshmfence-1.3-8.fc34.x86_64                                   82/99 
  Verifying        : llvm-libs-12.0.1-1.fc34.x86_64                                   83/99 
  Verifying        : mesa-libgbm-21.1.7-1.fc34.x86_64                                 84/99 
  Verifying        : mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                         85/99 
  Verifying        : nspr-4.32.0-1.fc34.x86_64                                        86/99 
  Verifying        : nss-3.69.0-1.fc34.x86_64                                         87/99 
  Verifying        : nss-softokn-3.69.0-1.fc34.x86_64                                 88/99 
  Verifying        : nss-softokn-freebl-3.69.0-1.fc34.x86_64                          89/99 
  Verifying        : nss-sysinit-3.69.0-1.fc34.x86_64                                 90/99 
  Verifying        : nss-util-3.69.0-1.fc34.x86_64                                    91/99 
  Verifying        : opus-1.3.1-8.fc34.x86_64                                         92/99 
  Verifying        : pango-1.48.9-2.fc34.x86_64                                       93/99 
  Verifying        : pixman-0.40.0-3.fc34.x86_64                                      94/99 
  Verifying        : pulseaudio-libs-14.2-3.fc34.x86_64                               95/99 
  Verifying        : sound-theme-freedesktop-0.8-15.fc34.noarch                       96/99 
  Verifying        : vulkan-loader-1.2.162.0-2.fc34.x86_64                            97/99 
  Verifying        : xdg-utils-1.1.3-9.fc34.noarch                                    98/99 
  Verifying        : xml-common-0.6.3-56.fc34.noarch                                  99/99 

Removed:
  adwaita-cursor-theme-40.1.1-1.fc34.noarch                                                 
  adwaita-icon-theme-40.1.1-1.fc34.noarch                                                   
  alsa-lib-1.2.5.1-2.fc34.x86_64                                                            
  at-spi2-atk-2.38.0-2.fc34.x86_64                                                          
  at-spi2-core-2.40.3-1.fc34.x86_64                                                         
  atk-2.36.0-3.fc34.x86_64                                                                  
  avahi-libs-0.8-14.fc34.x86_64                                                             
  cairo-1.17.4-3.fc34.x86_64                                                                
  cairo-gobject-1.17.4-3.fc34.x86_64                                                        
  colord-libs-1.4.5-2.fc34.x86_64                                                           
  cups-libs-1:2.3.3op2-7.fc34.x86_64                                                        
  dbus-libs-1:1.12.20-3.fc34.x86_64                                                         
  dconf-0.40.0-3.fc34.x86_64                                                                
  desktop-file-utils-0.26-3.fc34.x86_64                                                     
  emacs-filesystem-1:27.2-5.fc34.noarch                                                     
  flac-libs-1.3.3-7.fc34.x86_64                                                             
  fontconfig-2.13.94-2.fc34.x86_64                                                          
  freetype-2.10.4-3.fc34.x86_64                                                             
  fribidi-1.0.10-4.fc34.x86_64                                                              
  gdk-pixbuf2-2.42.6-1.fc34.x86_64                                                          
  gdk-pixbuf2-modules-2.42.6-1.fc34.x86_64                                                  
  google-chrome-stable-93.0.4577.63-1.x86_64                                                
  graphite2-1.3.14-7.fc34.x86_64                                                            
  gsm-1.0.19-5.fc34.x86_64                                                                  
  gstreamer1-1.19.1-2.1.18.4.fc34.x86_64                                                    
  gtk-update-icon-cache-3.24.30-1.fc34.x86_64                                               
  gtk3-3.24.30-1.fc34.x86_64                                                                
  harfbuzz-2.7.4-3.fc34.x86_64                                                              
  hicolor-icon-theme-0.17-10.fc34.noarch                                                    
  hwdata-0.351-1.fc34.noarch                                                                
  jbigkit-libs-2.1-21.fc34.x86_64                                                           
  lcms2-2.12-1.fc34.x86_64                                                                  
  libICE-1.0.10-6.fc34.x86_64                                                               
  libSM-1.2.3-8.fc34.x86_64                                                                 
  libX11-1.7.2-3.fc34.x86_64                                                                
  libX11-common-1.7.2-3.fc34.noarch                                                         
  libX11-xcb-1.7.2-3.fc34.x86_64                                                            
  libXau-1.0.9-6.fc34.x86_64                                                                
  libXcomposite-0.4.5-5.fc34.x86_64                                                         
  libXcursor-1.2.0-5.fc34.x86_64                                                            
  libXdamage-1.1.5-5.fc34.x86_64                                                            
  libXext-1.3.4-6.fc34.x86_64                                                               
  libXfixes-6.0.0-1.fc34.x86_64                                                             
  libXft-2.3.3-6.fc34.x86_64                                                                
  libXi-1.7.10-6.fc34.x86_64                                                                
  libXinerama-1.1.4-8.fc34.x86_64                                                           
  libXrandr-1.5.2-6.fc34.x86_64                                                             
  libXrender-0.9.10-14.fc34.x86_64                                                          
  libXtst-1.2.3-14.fc34.x86_64                                                              
  libasyncns-0.8-20.fc34.x86_64                                                             
  libcanberra-0.30-24.fc34.x86_64                                                           
  libcanberra-gtk3-0.30-24.fc34.x86_64                                                      
  libcloudproviders-0.3.1-3.fc34.x86_64                                                     
  libdatrie-0.2.13-1.fc34.x86_64                                                            
  libdrm-2.4.107-1.fc34.x86_64                                                              
  libedit-3.1-38.20210714cvs.fc34.x86_64                                                    
  libepoxy-1.5.9-1.fc34.x86_64                                                              
  liberation-fonts-1:2.1.4-1.fc34.noarch                                                    
  liberation-fonts-common-1:2.1.4-1.fc34.noarch                                             
  liberation-mono-fonts-1:2.1.4-1.fc34.noarch                                               
  liberation-sans-fonts-1:2.1.4-1.fc34.noarch                                               
  liberation-serif-fonts-1:2.1.4-1.fc34.noarch                                              
  libevent-2.1.12-3.fc34.x86_64                                                             
  libgusb-0.3.7-1.fc34.x86_64                                                               
  libjpeg-turbo-2.0.90-2.fc34.x86_64                                                        
  libogg-2:1.3.4-4.fc34.x86_64                                                              
  libpciaccess-0.16-4.fc34.x86_64                                                           
  libpng-2:1.6.37-10.fc34.x86_64                                                            
  libsndfile-1.0.31-5.fc34.fc34.x86_64                                                      
  libtdb-1.4.3-6.fc34.x86_64                                                                
  libthai-0.1.28-6.fc34.x86_64                                                              
  libtiff-4.2.0-1.fc34.x86_64                                                               
  libtool-ltdl-2.4.6-40.fc34.x86_64                                                         
  libunwind-1.4.0-5.fc34.x86_64                                                             
  libvorbis-1:1.3.7-3.fc34.x86_64                                                           
  libwayland-client-1.19.0-1.fc34.x86_64                                                    
  libwayland-cursor-1.19.0-1.fc34.x86_64                                                    
  libwayland-egl-1.19.0-1.fc34.x86_64                                                       
  libwayland-server-1.19.0-1.fc34.x86_64                                                    
  libwebp-1.2.1-1.fc34.x86_64                                                               
  libxcb-1.13.1-7.fc34.x86_64                                                               
  libxshmfence-1.3-8.fc34.x86_64                                                            
  llvm-libs-12.0.1-1.fc34.x86_64                                                            
  mesa-libgbm-21.1.7-1.fc34.x86_64                                                          
  mesa-vulkan-drivers-21.1.7-1.fc34.x86_64                                                  
  nspr-4.32.0-1.fc34.x86_64                                                                 
  nss-3.69.0-1.fc34.x86_64                                                                  
  nss-softokn-3.69.0-1.fc34.x86_64                                                          
  nss-softokn-freebl-3.69.0-1.fc34.x86_64                                                   
  nss-sysinit-3.69.0-1.fc34.x86_64                                                          
  nss-util-3.69.0-1.fc34.x86_64                                                             
  opus-1.3.1-8.fc34.x86_64                                                                  
  pango-1.48.9-2.fc34.x86_64                                                                
  pixman-0.40.0-3.fc34.x86_64                                                               
  pulseaudio-libs-14.2-3.fc34.x86_64                                                        
  sound-theme-freedesktop-0.8-15.fc34.noarch                                                
  vulkan-loader-1.2.162.0-2.fc34.x86_64                                                     
  xdg-utils-1.1.3-9.fc34.noarch                                                             
  xml-common-0.6.3-56.fc34.noarch                                                           

Complete!
```

## How can you list all the installed packages using RPM?

```bash
Using rpm -qa

[root@6b6ff9f9bc2d /]# rpm -qa
libgcc-11.1.1-3.fc34.x86_64
crypto-policies-20210213-1.git5c710c0.fc34.noarch
tzdata-2021a-1.fc34.noarch
fedora-release-identity-container-34-1.noarch
python-setuptools-wheel-53.0.0-2.fc34.noarch
libreport-filesystem-2.15.2-2.fc34.noarch
dnf-data-4.8.0-1.fc34.noarch
fedora-gpg-keys-34-2.noarch
fedora-repos-34-2.noarch
fedora-release-container-34-1.noarch
fedora-release-common-34-1.noarch
setup-2.13.7-3.fc34.noarch
filesystem-3.14-5.fc34.x86_64
basesystem-11-11.fc34.noarch
coreutils-common-8.32-30.fc34.x86_64
publicsuffix-list-dafsa-20190417-5.fc34.noarch
pcre2-syntax-10.36-4.fc34.noarch
ncurses-base-6.2-4.20200222.fc34.noarch
bash-5.1.0-2.fc34.x86_64
ncurses-libs-6.2-4.20200222.fc34.x86_64
glibc-common-2.33-20.fc34.x86_64
glibc-minimal-langpack-2.33-20.fc34.x86_64
glibc-2.33-20.fc34.x86_64
zlib-1.2.11-26.fc34.x86_64
bzip2-libs-1.0.8-6.fc34.x86_64
xz-libs-5.2.5-5.fc34.x86_64
libzstd-1.5.0-1.fc34.x86_64
sqlite-libs-3.34.1-2.fc34.x86_64
libcap-2.48-2.fc34.x86_64
libxcrypt-4.4.23-1.fc34.x86_64
gmp-6.2.0-6.fc34.x86_64
libcom_err-1.45.6-5.fc34.x86_64
libgpg-error-1.42-1.fc34.x86_64
libuuid-2.36.2-1.fc34.x86_64
popt-1.18-4.fc34.x86_64
libxml2-2.9.12-4.fc34.x86_64
readline-8.1-2.fc34.x86_64
lua-libs-5.4.3-1.fc34.x86_64
elfutils-libelf-0.185-2.fc34.x86_64
file-libs-5.39-6.fc34.x86_64
libattr-2.5.1-1.fc34.x86_64
libacl-2.3.1-1.fc34.x86_64
libffi-3.1-28.fc34.x86_64
p11-kit-0.23.22-3.fc34.x86_64
libsmartcols-2.36.2-1.fc34.x86_64
libunistring-0.9.10-10.fc34.x86_64
libidn2-2.3.1-1.fc34.x86_64
expat-2.4.1-1.fc34.x86_64
libstdc++-11.1.1-3.fc34.x86_64
libassuan-2.5.5-1.fc34.x86_64
libgcrypt-1.9.3-3.fc34.x86_64
alternatives-1.15-2.fc34.x86_64
json-c-0.14-8.fc34.x86_64
keyutils-libs-1.6.1-2.fc34.x86_64
libcap-ng-0.8.2-4.fc34.x86_64
audit-libs-3.0.2-1.fc34.x86_64
libdb-5.3.28-46.fc34.x86_64
libsepol-3.2-1.fc34.x86_64
libtasn1-4.16.0-4.fc34.x86_64
p11-kit-trust-0.23.22-3.fc34.x86_64
lz4-libs-1.9.3-2.fc34.x86_64
pcre-8.44-3.fc34.1.x86_64
grep-3.6-2.fc34.x86_64
pcre2-10.36-4.fc34.x86_64
libselinux-3.2-1.fc34.x86_64
sed-4.8-7.fc34.x86_64
openssl-libs-1.1.1k-1.fc34.x86_64
coreutils-8.32-30.fc34.x86_64
ca-certificates-2021.2.50-1.0.fc34.noarch
libblkid-2.36.2-1.fc34.x86_64
libmount-2.36.2-1.fc34.x86_64
glib2-2.68.2-1.fc34.x86_64
systemd-libs-248.5-1.fc34.x86_64
zchunk-libs-1.1.15-1.fc34.x86_64
libusbx-1.0.24-2.fc34.x86_64
libfdisk-2.36.2-1.fc34.x86_64
python-pip-wheel-21.0.1-3.fc34.noarch
gzip-1.10-4.fc34.x86_64
cracklib-2.9.6-25.fc34.x86_64
libarchive-3.5.1-2.fc34.x86_64
libsemanage-3.2-1.fc34.x86_64
shadow-utils-4.8.1-8.fc34.x86_64
libutempter-1.2.1-4.fc34.x86_64
vim-minimal-8.2.3182-1.fc34.x86_64
libmetalink-0.1.3-14.fc34.x86_64
libcomps-0.1.17-1.fc34.x86_64
libpsl-0.21.1-3.fc34.x86_64
libksba-1.5.0-2.fc34.x86_64
mpfr-4.1.0-7.fc34.x86_64
nettle-3.7.3-1.fc34.x86_64
gnutls-3.7.2-1.fc34.x86_64
gdbm-libs-1.19-2.fc34.x86_64
libbrotli-1.0.9-4.fc34.x86_64
libnghttp2-1.43.0-2.fc34.x86_64
libsigsegv-2.13-2.fc34.x86_64
gawk-5.1.0-3.fc34.x86_64
libverto-0.3.2-1.fc34.x86_64
krb5-libs-1.19.1-14.fc34.x86_64
libtirpc-1.3.2-0.fc34.x86_64
libnsl2-1.3.0-2.fc34.x86_64
python3-3.9.6-2.fc34.x86_64
python3-libs-3.9.6-2.fc34.x86_64
python3-libcomps-0.1.17-1.fc34.x86_64
cyrus-sasl-lib-2.1.27-8.fc34.x86_64
openldap-2.4.57-5.fc34.x86_64
libyaml-0.2.5-5.fc34.x86_64
npth-1.6-6.fc34.x86_64
gnupg2-2.2.27-4.fc34.x86_64
gpgme-1.15.1-2.fc34.x86_64
python3-gpg-1.15.1-2.fc34.x86_64
libeconf-0.4.0-1.fc34.x86_64
libpwquality-1.4.4-2.fc34.x86_64
pam-1.5.1-6.fc34.x86_64
libgomp-11.1.1-3.fc34.x86_64
libsss_idmap-2.5.1-2.fc34.x86_64
libsss_nss_idmap-2.5.1-2.fc34.x86_64
elfutils-default-yama-scope-0.185-2.fc34.noarch
elfutils-libs-0.185-2.fc34.x86_64
libssh-config-0.9.5-2.fc34.noarch
libssh-0.9.5-2.fc34.x86_64
libcurl-7.76.1-4.fc34.x86_64
curl-7.76.1-4.fc34.x86_64
rpm-libs-4.16.1.3-1.fc34.x86_64
rpm-4.16.1.3-1.fc34.x86_64
libsolv-0.7.17-3.fc34.x86_64
libmodulemd-2.13.0-1.fc34.x86_64
rpm-build-libs-4.16.1.3-1.fc34.x86_64
librepo-1.14.1-1.fc34.x86_64
libdnf-0.63.1-1.fc34.x86_64
python3-libdnf-0.63.1-1.fc34.x86_64
python3-hawkey-0.63.1-1.fc34.x86_64
tpm2-tss-3.1.0-1.fc34.x86_64
ima-evm-utils-1.3.2-2.fc34.x86_64
rpm-sign-libs-4.16.1.3-1.fc34.x86_64
python3-rpm-4.16.1.3-1.fc34.x86_64
python3-dnf-4.8.0-1.fc34.noarch
dnf-4.8.0-1.fc34.noarch
fonts-filesystem-2.0.5-5.fc34.noarch
dejavu-sans-fonts-2.37-16.fc34.noarch
langpacks-core-font-en-3.0-14.fc34.noarch
langpacks-core-en_GB-3.0-14.fc34.noarch
langpacks-en_GB-3.0-14.fc34.noarch
yum-4.8.0-1.fc34.noarch
sssd-client-2.5.1-2.fc34.x86_64
sudo-1.9.5p2-1.fc34.x86_64
util-linux-2.36.2-1.fc34.x86_64
tar-1.34-1.fc34.x86_64
fedora-repos-modular-34-2.noarch
rootfiles-8.1-29.fc34.noarch
gpg-pubkey-45719a39-5f2c0192
wget-1.21.1-3.fc34.x86_64
```