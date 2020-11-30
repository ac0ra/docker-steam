# Use the empty image with the portage tree as the first stage
FROM gentoo/portage:latest as portage

# Gentoo stage3 is the second stage, basically an unpacked Gentoo Linux
FROM gentoo/stage3:latest as gentoo

# Copy the portage tree into the current stage
COPY --from=portage /var/db/repos /var/db/repos


RUN emerge eix vim dev-vcs/git
RUN wget -P /etc/portage/repos.conf/ https://raw.githubusercontent.com/anyc/steam-overlay/master/steam-overlay.conf
RUN emaint sync --repo steam-overlay
COPY rootfs/etc/portage/package.use /etc/portage/package.use
COPY rootfs/etc/portage/package.keywords /etc/portage/package.accept_keywords
COPY rootfs/etc/portage/package.license /etc/portage/package.license
COPY rootfs/etc/portage/make.conf /etc/portage/make.conf
RUN emerge -DNU steam-launcher
RUN emerge -DNu mesa vulkan-loader pulseaudio vulkan-tools vulkan-headers

