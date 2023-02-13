WHEN I went to look at this repo, the README says that this is deprecated for:
`This Repository is deprecated in favor of https://github.com/giggls/osml10n/`

* [x] use `https://github.com/giggls/osml10n/` instead
??should I uninstall it, it worked with the deprecated version but I only found out after I first installed this one.

Install OSM Localization Extension (osml10n)
cd ~

git clone https://github.com/giggls/mapnik-german-l10n

cd mapnik-german-l10n/

sudo apt install devscripts equivs python3 python3-pip -y

sudo mk-build-deps -i debian/control

sudo pip3 install tltk

make deb

sudo apt install ../postgresql*osml10n*amd64.deb
The extension will be installed under /usr/share/postgresql/15/extension/.

WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

I got this trying to run `sudo pip3 install `sudo pip3 install tltk`

drifter@vmi1120784:~$ ls
osml10n  osml10n_1.0_all.deb  osml10n_1.0_amd64.buildinfo  osml10n_1.0_amd64.changes  pgsql-gzip

These were the files in my ~ directory before I did the german git clone

...

and now there are these:
drifter@vmi1120784:~$ ls
mapnik-german-l10n  osml10n_1.0_all.deb          osml10n_1.0_amd64.changes       osml10n_2.5.10_amd64.changes  postgresql-15-osml10n_2.5.10_amd64.deb
osml10n             osml10n_1.0_amd64.buildinfo  osml10n_2.5.10_amd64.buildinfo  pgsql-gzip                    postgresql-15-osml10n-dbgsym_2.5.10_amd64.ddeb

