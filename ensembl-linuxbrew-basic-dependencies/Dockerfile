# Docker image with all necessary Homebrew and Ensembl taps
FROM linuxbrew/brew:3.0.0

# Setup moonshine
ENV HOMEBREW_ENSEMBL_MOONSHINE_ARCHIVE /home/linuxbrew/ENSEMBL_MOONSHINE_ARCHIVE
RUN mkdir -p $HOMEBREW_ENSEMBL_MOONSHINE_ARCHIVE

# Turning off autoupdate
ENV HOMEBREW_NO_AUTO_UPDATE 1

# Turn off analytics and tap brew & Ensembl repositories
# I need to patch to use openjdk instead of jdk. Not using -i so it can work on Mac and Linux
RUN brew analytics off \
&& brew tap denji/nginx \
&& brew tap ensembl/ensembl \
&& brew tap ensembl/external \
&& brew tap ensembl/moonshine \
&& brew tap ensembl/cask \
&& sed -i 's/jdk/openjdk/g' /home/linuxbrew/.linuxbrew/Homebrew/Library/Taps/ensembl/homebrew-cask/pre-flight.rb \
&& sed -i '/mysql-cluster/d;s/because =>/because/g' /home/linuxbrew/.linuxbrew/Homebrew/Library/Taps/ensembl/homebrew-external/percona-client.rb

RUN brew install ensembl/cask/pre-flight \
&& brew install ensembl/cask/basic-dependencies \
&& brew install ensembl/cask/perl-clibs \
&& brew cleanup \
&& rm -rf /home/linuxbrew/.cpan /home/linuxbrew/.cache/Homebrew
