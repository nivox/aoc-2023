FROM gitpod/workspace-base

SHELL ["/bin/bash", "-c"]
USER gitpod
ENV USER=gitpod

# Common
RUN bash <(curl -L https://nixos.org/nix/install) --no-daemon
RUN mkdir -p ~/.config/nix && echo "experimental-features = nix-command flakes" > ~/.config/nix/nix.conf
RUN . /home/gitpod/.nix-profile/etc/profile.d/nix.sh \
	&& nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager \
	&& nix-channel --update \
	&& nix-shell '<home-manager>' -A install

RUN echo ". /home/gitpod/.nix-profile/etc/profile.d/nix.sh" >> ~/.bashrc \
	&& echo ". $HOME/.nix-profile/etc/profile.d/hm-session-vars.sh" >> ~/.bashrc

	
# Repo specific
RUN . /home/gitpod/.nix-profile/etc/profile.d/nix.sh \
	&& nix profile install nixpkgs#rustup \
  	&& rustup default stable \
  	&& rustup component add rust-analyzer