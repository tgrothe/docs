### Links:

- https://wiki.archlinux.org/title/fprint
- https://aur.archlinux.org/packages/yay
- https://github.com/uunicorn/python-validity
- https://wiki.archlinux.org/title/PAM
- https://wiki.archlinux.org/title/Fprint#Login_configuration
- https://wiki.archlinux.org/title/SDDM#Using_a_fingerprint_reader

### Prerequisites:

Make sure you can see the connected sensor by typing `lsusb`.

### Steps:

1. Run `sudo pacman -Syu base-devel git`

1. Add AUR-Support as third-party source in "Add Software..."

1. Install yay by typing `sudo pacman -Syu yay`

1. Install python-validity by typing `yay -S python-validity`

1. Check service status with `sudo systemctl status python3-validity`

1. Start service with `sudo systemctl start python3-validity`

1. Run `fprintd-enroll` to enroll a finger

1. Check everything works fine with `fprintd-verify`

1. Add the following line to the top of `/etc/pam.d/sudo`:

        auth      sufficient pam_fprintd.so

1. Add the following two lines at the top of the files: `login`, `system-local-login`, `system-login`, `system-auth` (and `sddm`):

        auth		sufficient  	pam_unix.so try_first_pass likeauth nullok
        auth		sufficient  	pam_fprintd.so

Now everything should work fine.
You should be first asked for your PWD;
but by typing Enter, you should be asked
for your fingerprint scan; except for sudo requests:
here you should only be asked for fingerprint scan.
