FROM archlinux:base-devel AS mkdocs-builder

RUN pacman -Syuu --noconfirm git mkdocs  \
    python-csscompressor pngquant python-cairosvg python-colorama  \
    python-hatch-nodejs-version python-hatch-requirements-txt \
    python-regex python-xcffib python-sphinx python-setuptools python-pytest
COPY --chmod=777 aur /bin/aur

# Can't build from the AUR as root
RUN useradd -m -G wheel aur-builder
COPY --chmod=755 sudoers /etc/sudoers
USER aur-builder

WORKDIR /home/aur-builder
RUN aur python-htmlmin2
RUN aur python-jsmin
RUN aur mkdocs-minify-plugin
RUN aur pymdown-extensions
RUN aur python-paginate
RUN aur mkdocs-redirects
RUN aur mkdocs-material-extensions
RUN aur mkdocs-material

FROM archlinux:base

COPY --chmod=777 install-mkdocs /bin/install-mkdocs
COPY --from=mkdocs-builder /home/aur-builder/pkgs /opt/pkgs
RUN install-mkdocs
