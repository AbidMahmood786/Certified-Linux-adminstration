# Chapter 10: Podman Containers
CHAPTER 10 — Podman Containers (RHCSA Exam‑Focused)
(Podman is heavily tested in RHEL 9)
1. RHCSA Objectives

Manage rootless and rootful containers
Pull, run, stop, remove images and containers
Manage volumes for persistence
Build container images
Create systemd units for containers
Understand Podman vs Docker differences


2. Essential Commands
Images
podman search httpd
podman pull registry.access.redhat.com/ubi8/httpd-24
podman images
podman rmi <image>

Containers
podman run -d --name web -p 8080:80 httpd
podman ps
podman ps -a
podman stop web
podman rm web

Volumes (Exam Important)
podman volume create webdata
podman run -d --name web -v webdata:/var/www/html httpd
podman volume inspect webdata

Systemd Unit Generation
podman generate systemd --name web --files
systemctl --user enable --now container-web.service


3. Fast Theory

Podman is daemonless (unlike Docker)
Rootless containers run under user namespace
Images use layered storage
Volume mapping ensures persistence:
-v hostdir:containerdir


Podman can auto‑generate systemd units for container auto‑start at boot
Podman stores data under:

Rootless: $HOME/.local/share/containers
Rootful: /var/lib/containers




4. RHCSA Labs
Lab 1 — Pull and Run Container
podman pull nginx
podman run -d --name web -p 8080:80 nginx
podman ps


Lab 2 — Persistent Storage with Volumes
podman volume create webdata
podman run -d --name web -v webdata:/usr/share/nginx/html -p 8080:80 nginx

Validate:
Create file inside volume and refresh browser.

Lab 3 — Stop and Remove Container
podman stop web
podman rm web
podman ps -a


Lab 4 — Generate systemd Unit
podman generate systemd --name web --files
cp container-web.service ~/.config/systemd/user/
systemctl --user daemon-reload
systemctl --user enable --now container-web.service


5. Troubleshooting

























IssueReasonFix8080 already usedPort conflictss -tlnpContainer can’t writeNo volume or permsAdd -v correctlySystemd service failsWrong file locationPut under ~/.config/systemd/user/

6. MCQs


Which command lists running containers?
A) podman list B) docker ps C) podman ps D) ctr ps
Answer: C


Podman is:
A) Daemon-based B) Daemonless C) Cloud service D) Systemd‑only
Answer: B


Create volume:
A) podman vol new
B) podman create vol
C) podman volume create
D) podman create --volume
Answer: C


Persistent storage is mounted with:
A) -mount
B) -store
C) --data
D) -v
Answer: D


Autostart container at boot:
A) podman auto
B) podman reboot
C) systemd unit
D) initctl podman
Answer: C
