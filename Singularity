# Generated by Neurodocker version 0.4.2-3-gf7055a1
# Timestamp: 2020-06-29 18:20:45 UTC
#
# Thank you for using Neurodocker. If you discover any issues
# or ways to improve this software, please submit an issue or
# pull request on our GitHub repository:
#
#     https://github.com/kaczmarj/neurodocker

Bootstrap: docker
From: ubuntu:xenial

%post
export ND_ENTRYPOINT="/neurodocker/startup.sh"
apt-get update -qq
apt-get install -y -q --no-install-recommends \
    apt-utils \
    bzip2 \
    ca-certificates \
    curl \
    locales \
    unzip
apt-get clean
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
dpkg-reconfigure --frontend=noninteractive locales
update-locale LANG="en_US.UTF-8"
chmod 777 /opt && chmod a+s /opt
mkdir -p /neurodocker
if [ ! -f "$ND_ENTRYPOINT" ]; then
  echo '#!/usr/bin/env bash' >> "$ND_ENTRYPOINT"
  echo 'set -e' >> "$ND_ENTRYPOINT"
  echo 'if [ -n "$1" ]; then "$@"; else /usr/bin/env bash; fi' >> "$ND_ENTRYPOINT";
fi
chmod -R 777 /neurodocker && chmod a+s /neurodocker

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    tcsh \
    bc \
    tar \
    libgomp1 \
    perl-modules \
    wget \
    curl \
    libsm-dev \
    libx11-dev \
    libxt-dev \
    libxext-dev \
    libglu1-mesa \
    libpython2.7-stdlib
apt-get clean
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    bc \
    libgomp1 \
    libxmu6 \
    libxt6 \
    perl \
    tcsh
apt-get clean
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
echo "Downloading FreeSurfer ..."
mkdir -p /opt/freesurfer
curl -fsSL --retry 5 ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz \
| tar -xz -C /opt/freesurfer --strip-components 1 \
  --exclude='freesurfer/average/mult-comp-cor' \
  --exclude='freesurfer/lib/cuda' \
  --exclude='freesurfer/lib/qt' \
  --exclude='freesurfer/subjects/V1_average' \
  --exclude='freesurfer/subjects/bert' \
  --exclude='freesurfer/subjects/cvs_avg35' \
  --exclude='freesurfer/subjects/cvs_avg35_inMNI152' \
  --exclude='freesurfer/subjects/fsaverage3' \
  --exclude='freesurfer/subjects/fsaverage4' \
  --exclude='freesurfer/subjects/fsaverage5' \
  --exclude='freesurfer/subjects/fsaverage6' \
  --exclude='freesurfer/subjects/fsaverage_sym' \
  --exclude='freesurfer/trctrain'
sed -i '$isource "/opt/freesurfer/SetUpFreeSurfer.sh"' "$ND_ENTRYPOINT"

export PATH="/opt/miniconda-latest/bin:$PATH"
echo "Downloading Miniconda installer ..."
conda_installer="/tmp/miniconda.sh"
curl -fsSL --retry 5 -o "$conda_installer" https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash "$conda_installer" -b -p /opt/miniconda-latest
rm -f "$conda_installer"
conda update -yq -nbase conda
conda config --system --prepend channels conda-forge
conda config --system --set auto_update_conda false
conda config --system --set show_channel_urls true
sync && conda clean -tipsy && sync
conda install -y -q --name base \
    'python=3' \
    'pip' \
    'pandas' \
    'setuptools' \
    'pandas=0.21.0'
sync && conda clean -tipsy && sync
bash -c "source activate base
  pip install --no-cache-dir  \
      'nibabel'"
rm -rf ~/.cache/pip/*
sync


bash -c 'curl -sL https://deb.nodesource.com/setup_6.x | bash -'

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    nodejs
apt-get clean
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

bash -c 'npm install -g bids-validator@0.19.8'

mkdir root/matlab && touch root/matlab/startup.m

mkdir /scratch

mkdir /local-scratch

chmod +x /run.py

echo '{
\n  "pkg_manager": "apt",
\n  "instructions": [
\n    [
\n      "base",
\n      "ubuntu:xenial"
\n    ],
\n    [
\n      "_header",
\n      {
\n        "version": "generic",
\n        "method": "custom"
\n      }
\n    ],
\n    [
\n      "install",
\n      [
\n        "tcsh",
\n        "bc",
\n        "tar",
\n        "libgomp1",
\n        "perl-modules",
\n        "wget",
\n        "curl",
\n        "libsm-dev",
\n        "libx11-dev",
\n        "libxt-dev",
\n        "libxext-dev",
\n        "libglu1-mesa",
\n        "libpython2.7-stdlib"
\n      ]
\n    ],
\n    [
\n      "freesurfer",
\n      {
\n        "version": "6.0.1",
\n        "install_path": "/opt/freesurfer"
\n      }
\n    ],
\n    [
\n      "miniconda",
\n      {
\n        "use_env": "base",
\n        "conda_install": [
\n          "python=3",
\n          "pip",
\n          "pandas",
\n          "setuptools",
\n          "pandas=0.21.0"
\n        ],
\n        "pip_install": [
\n          "nibabel"
\n        ]
\n      }
\n    ],
\n    [
\n      "run_bash",
\n      "curl -sL https://deb.nodesource.com/setup_6.x | bash -"
\n    ],
\n    [
\n      "install",
\n      [
\n        "nodejs"
\n      ]
\n    ],
\n    [
\n      "run_bash",
\n      "npm install -g bids-validator@0.19.8"
\n    ],
\n    [
\n      "env",
\n      {
\n        "FSLDIR": "/usr/share/fsl/5.0",
\n        "FSLOUTPUTTYPE": "NIFTI_GZ",
\n        "FSLMULTIFILEQUIT": "TRUE",
\n        "POSSUMDIR": "/usr/share/fsl/5.0",
\n        "LD_LIBRARY_PATH": "/usr/lib/fsl/5.0:",
\n        "FSLTCLSH": "/usr/bin/tclsh",
\n        "FSLWISH": "/usr/bin/wish"
\n      }
\n    ],
\n    [
\n      "env",
\n      {
\n        "OS": "Linux",
\n        "FS_OVERRIDE": "0",
\n        "FIX_VERTEX_AREA": "",
\n        "SUBJECTS_DIR": "/opt/freesurfer/subjects",
\n        "FSF_OUTPUT_FORMAT": "nii.gz",
\n        "MNI_DIR": "/opt/freesurfer/mni",
\n        "LOCAL_DIR": "/opt/freesurfer/local",
\n        "FREESURFER_HOME": "/opt/freesurfer",
\n        "FSFAST_HOME": "/opt/freesurfer/fsfast",
\n        "MINC_BIN_DIR": "/opt/freesurfer/mni/bin",
\n        "MINC_LIB_DIR": "/opt/freesurfer/mni/lib",
\n        "MNI_DATAPATH": "/opt/freesurfer/mni/data",
\n        "FMRI_ANALYSIS_DIR": "/opt/freesurfer/fsfast",
\n        "PERL5LIB": "/opt/freesurfer/mni/share/perl5",
\n        "MNI_PERL5LIB": "/opt/freesurfer/mni/share/perl5/",
\n        "PATH": "/opt/miniconda-latest/bin:/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:/usr/lib/fsl/5.0:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
\n        "PYTHONPATH": ""
\n      }
\n    ],
\n    [
\n      "run",
\n      "mkdir root/matlab && touch root/matlab/startup.m"
\n    ],
\n    [
\n      "run",
\n      "mkdir /scratch"
\n    ],
\n    [
\n      "run",
\n      "mkdir /local-scratch"
\n    ],
\n    [
\n      "copy",
\n      [
\n        "run.py",
\n        "/run.py"
\n      ]
\n    ],
\n    [
\n      "run",
\n      "chmod +x /run.py"
\n    ],
\n    [
\n      "copy",
\n      [
\n        "version",
\n        "/version"
\n      ]
\n    ],
\n    [
\n      "entrypoint",
\n      "/neurodocker/startup.sh /run.py"
\n    ]
\n  ]
\n}' > /neurodocker/neurodocker_specs.json

%environment
export LANG="en_US.UTF-8"
export LC_ALL="en_US.UTF-8"
export ND_ENTRYPOINT="/neurodocker/startup.sh"
export FREESURFER_HOME="/opt/freesurfer"
export PATH="/opt/freesurfer/bin:$PATH"
export CONDA_DIR="/opt/miniconda-latest"
export PATH="/opt/miniconda-latest/bin:$PATH"
export FSLDIR="/usr/share/fsl/5.0"
export FSLOUTPUTTYPE="NIFTI_GZ"
export FSLMULTIFILEQUIT="TRUE"
export POSSUMDIR="/usr/share/fsl/5.0"
export LD_LIBRARY_PATH="/usr/lib/fsl/5.0:"
export FSLTCLSH="/usr/bin/tclsh"
export FSLWISH="/usr/bin/wish"
export OS="Linux"
export FS_OVERRIDE="0"
export FIX_VERTEX_AREA=""
export SUBJECTS_DIR="/opt/freesurfer/subjects"
export FSF_OUTPUT_FORMAT="nii.gz"
export MNI_DIR="/opt/freesurfer/mni"
export LOCAL_DIR="/opt/freesurfer/local"
export FREESURFER_HOME="/opt/freesurfer"
export FSFAST_HOME="/opt/freesurfer/fsfast"
export MINC_BIN_DIR="/opt/freesurfer/mni/bin"
export MINC_LIB_DIR="/opt/freesurfer/mni/lib"
export MNI_DATAPATH="/opt/freesurfer/mni/data"
export FMRI_ANALYSIS_DIR="/opt/freesurfer/fsfast"
export PERL5LIB="/opt/freesurfer/mni/share/perl5"
export MNI_PERL5LIB="/opt/freesurfer/mni/share/perl5/"
export PATH="/opt/miniconda-latest/bin:/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:/usr/lib/fsl/5.0:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
export PYTHONPATH=""

%files
run.py /run.py
version /version

%runscript
/neurodocker/startup.sh /run.py
