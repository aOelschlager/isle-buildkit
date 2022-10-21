# syntax=docker/dockerfile:1.2.1
ARG repository=local
ARG tag=latest
FROM --platform=$BUILDPLATFORM ${repository}/download:${tag} AS download

ARG COMMIT=bbdcfd203789ebd0e9a27e00a4036404e36c789f

RUN --mount=type=cache,id=crayfish-downloads,sharing=locked,target=/opt/downloads \
    git-clone-cached.sh \
        --url https://github.com/nigelgbanks/Crayfish.git \
        --cache-dir "${DOWNLOAD_CACHE_DIRECTORY}" \
        --commit "${COMMIT}" \
        --worktree /var/www/crayfish

FROM ${repository}/composer:${tag}

COPY --from=download --chown=nginx:nginx /var/www /var/www

COPY rootfs /
