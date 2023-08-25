# Generated by Neurodocker and Reproenv.

Bootstrap: docker
From: ubuntu:jammy

%files
run.py /run.py
version /version

%environment
export OS="Linux"
export PATH="/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:$PATH"
export FREESURFER_HOME="/opt/freesurfer"
export FREESURFER="/opt/freesurfer"
export SUBJECTS_DIR="/opt/freesurfer/subjects"
export LOCAL_DIR="/opt/freesurfer/local"
export FSFAST_HOME="/opt/freesurfer/fsfast"
export FMRI_ANALYSIS_DIR="/opt/freesurfer/fsfast"
export FUNCTIONALS_DIR="/opt/freesurfer/sessions"
export FS_OVERRIDE="0"
export FIX_VERTEX_AREA=""
export FSF_OUTPUT_FORMAT="nii.gz# mni env requirements"
export MINC_BIN_DIR="/opt/freesurfer/mni/bin"
export MINC_LIB_DIR="/opt/freesurfer/mni/lib"
export MNI_DIR="/opt/freesurfer/mni"
export MNI_DATAPATH="/opt/freesurfer/mni/data"
export MNI_PERL5LIB="/opt/freesurfer/mni/share/perl5"
export PERL5LIB="/opt/freesurfer/mni/share/perl5"
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

%post
apt-get update -qq
apt-get install -y -q --no-install-recommends \
    bc \
    curl \
    libglu1-mesa \
    libgomp1 \
    libpython2.7-stdlib \
    libsm-dev \
    libx11-dev \
    libxext-dev \
    libxt-dev \
    perl-modules \
    tar \
    tcsh \
    wget
rm -rf /var/lib/apt/lists/*

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    bc \
    ca-certificates \
    curl \
    libgomp1 \
    libxmu6 \
    libxt6 \
    perl \
    tcsh
rm -rf /var/lib/apt/lists/*
echo "Downloading FreeSurfer ..."
mkdir -p /opt/freesurfer
curl -fL ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz \
| tar -xz -C /opt/freesurfer --owner root --group root --no-same-owner --strip-components 1 \
  --exclude='average/mult-comp-cor' \
  --exclude='lib/cuda' \
  --exclude='lib/qt' \
  --exclude='subjects/V1_average' \
  --exclude='subjects/bert' \
  --exclude='subjects/cvs_avg35' \
  --exclude='subjects/cvs_avg35_inMNI152' \
  --exclude='subjects/fsaverage3' \
  --exclude='subjects/fsaverage4' \
  --exclude='subjects/fsaverage5' \
  --exclude='subjects/fsaverage6' \
  --exclude='subjects/fsaverage_sym' \
  --exclude='trctrain'

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    bzip2 \
    ca-certificates \
    curl
rm -rf /var/lib/apt/lists/*
# Install dependencies.
export PATH="/opt/miniconda-latest/bin:$PATH"
echo "Downloading Miniconda installer ..."
conda_installer="/tmp/miniconda.sh"
curl -fsSL -o "$conda_installer" https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash "$conda_installer" -b -p /opt/miniconda-latest
rm -f "$conda_installer"
conda update -yq -nbase conda
# Prefer packages in conda-forge
conda config --system --prepend channels conda-forge
# Packages in lower-priority channels not considered if a package with the same
# name exists in a higher priority channel. Can dramatically speed up installations.
# Conda recommends this as a default
# https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html
conda config --set channel_priority strict
conda config --system --set auto_update_conda false
conda config --system --set show_channel_urls true
# Enable `conda activate`
conda init bash
conda install -y  --name base \
    "python=3" \
    "pip" \
    "pandas" \
    "setuptools" \
    "pandas=0.21.0"
bash -c "source activate base
  python -m pip install --no-cache-dir  \
      "nibabel""
# Clean up
sync && conda clean --all --yes && sync
rm -rf ~/.cache/pip/*

bash -c 'curl -sL https://deb.nodesource.com/setup_6.x | bash -'

apt-get update -qq
apt-get install -y -q --no-install-recommends \
    nodejs
rm -rf /var/lib/apt/lists/*

bash -c 'npm install -g bids-validator@0.19.8'

mkdir root/matlab && touch root/matlab/startup.m

mkdir /scratch

mkdir /local-scratch

chmod +x /run.py

# Save specification to JSON.
printf '{ \
  "pkg_manager": "apt", \
  "existing_users": [ \
    "root" \
  ], \
  "instructions": [ \
    { \
      "name": "from_", \
      "kwds": { \
        "base_image": "ubuntu:jammy" \
      } \
    }, \
    { \
      "name": "install", \
      "kwds": { \
        "pkgs": [ \
          "tcsh", \
          "bc", \
          "tar", \
          "libgomp1", \
          "perl-modules", \
          "wget", \
          "curl", \
          "libsm-dev", \
          "libx11-dev", \
          "libxt-dev", \
          "libxext-dev", \
          "libglu1-mesa", \
          "libpython2.7-stdlib" \
        ], \
        "opts": null \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "apt-get update -qq\\napt-get install -y -q --no-install-recommends \\\\\\n    bc \\\\\\n    curl \\\\\\n    libglu1-mesa \\\\\\n    libgomp1 \\\\\\n    libpython2.7-stdlib \\\\\\n    libsm-dev \\\\\\n    libx11-dev \\\\\\n    libxext-dev \\\\\\n    libxt-dev \\\\\\n    perl-modules \\\\\\n    tar \\\\\\n    tcsh \\\\\\n    wget\\nrm -rf /var/lib/apt/lists/*" \
      } \
    }, \
    { \
      "name": "env", \
      "kwds": { \
        "OS": "Linux", \
        "PATH": "/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:$PATH", \
        "FREESURFER_HOME": "/opt/freesurfer", \
        "FREESURFER": "/opt/freesurfer", \
        "SUBJECTS_DIR": "/opt/freesurfer/subjects", \
        "LOCAL_DIR": "/opt/freesurfer/local", \
        "FSFAST_HOME": "/opt/freesurfer/fsfast", \
        "FMRI_ANALYSIS_DIR": "/opt/freesurfer/fsfast", \
        "FUNCTIONALS_DIR": "/opt/freesurfer/sessions", \
        "FS_OVERRIDE": "0", \
        "FIX_VERTEX_AREA": "", \
        "FSF_OUTPUT_FORMAT": "nii.gz# mni env requirements", \
        "MINC_BIN_DIR": "/opt/freesurfer/mni/bin", \
        "MINC_LIB_DIR": "/opt/freesurfer/mni/lib", \
        "MNI_DIR": "/opt/freesurfer/mni", \
        "MNI_DATAPATH": "/opt/freesurfer/mni/data", \
        "MNI_PERL5LIB": "/opt/freesurfer/mni/share/perl5", \
        "PERL5LIB": "/opt/freesurfer/mni/share/perl5" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "apt-get update -qq\\napt-get install -y -q --no-install-recommends \\\\\\n    bc \\\\\\n    ca-certificates \\\\\\n    curl \\\\\\n    libgomp1 \\\\\\n    libxmu6 \\\\\\n    libxt6 \\\\\\n    perl \\\\\\n    tcsh\\nrm -rf /var/lib/apt/lists/*\\necho \\"Downloading FreeSurfer ...\\"\\nmkdir -p /opt/freesurfer\\ncurl -fL ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz \\\\\\n| tar -xz -C /opt/freesurfer --owner root --group root --no-same-owner --strip-components 1 \\\\\\n  --exclude='"'"'average/mult-comp-cor'"'"' \\\\\\n  --exclude='"'"'lib/cuda'"'"' \\\\\\n  --exclude='"'"'lib/qt'"'"' \\\\\\n  --exclude='"'"'subjects/V1_average'"'"' \\\\\\n  --exclude='"'"'subjects/bert'"'"' \\\\\\n  --exclude='"'"'subjects/cvs_avg35'"'"' \\\\\\n  --exclude='"'"'subjects/cvs_avg35_inMNI152'"'"' \\\\\\n  --exclude='"'"'subjects/fsaverage3'"'"' \\\\\\n  --exclude='"'"'subjects/fsaverage4'"'"' \\\\\\n  --exclude='"'"'subjects/fsaverage5'"'"' \\\\\\n  --exclude='"'"'subjects/fsaverage6'"'"' \\\\\\n  --exclude='"'"'subjects/fsaverage_sym'"'"' \\\\\\n  --exclude='"'"'trctrain'"'"'" \
      } \
    }, \
    { \
      "name": "env", \
      "kwds": { \
        "CONDA_DIR": "/opt/miniconda-latest", \
        "PATH": "/opt/miniconda-latest/bin:$PATH" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "apt-get update -qq\\napt-get install -y -q --no-install-recommends \\\\\\n    bzip2 \\\\\\n    ca-certificates \\\\\\n    curl\\nrm -rf /var/lib/apt/lists/*\\n# Install dependencies.\\nexport PATH=\\"/opt/miniconda-latest/bin:$PATH\\"\\necho \\"Downloading Miniconda installer ...\\"\\nconda_installer=\\"/tmp/miniconda.sh\\"\\ncurl -fsSL -o \\"$conda_installer\\" https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh\\nbash \\"$conda_installer\\" -b -p /opt/miniconda-latest\\nrm -f \\"$conda_installer\\"\\nconda update -yq -nbase conda\\n# Prefer packages in conda-forge\\nconda config --system --prepend channels conda-forge\\n# Packages in lower-priority channels not considered if a package with the same\\n# name exists in a higher priority channel. Can dramatically speed up installations.\\n# Conda recommends this as a default\\n# https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html\\nconda config --set channel_priority strict\\nconda config --system --set auto_update_conda false\\nconda config --system --set show_channel_urls true\\n# Enable `conda activate`\\nconda init bash\\nconda install -y  --name base \\\\\\n    \\"python=3\\" \\\\\\n    \\"pip\\" \\\\\\n    \\"pandas\\" \\\\\\n    \\"setuptools\\" \\\\\\n    \\"pandas=0.21.0\\"\\nbash -c \\"source activate base\\n  python -m pip install --no-cache-dir  \\\\\\n      \\"nibabel\\"\\"\\n# Clean up\\nsync && conda clean --all --yes && sync\\nrm -rf ~/.cache/pip/*" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "bash -c '"'"'curl -sL https://deb.nodesource.com/setup_6.x | bash -'"'"'" \
      } \
    }, \
    { \
      "name": "install", \
      "kwds": { \
        "pkgs": [ \
          "nodejs" \
        ], \
        "opts": null \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "apt-get update -qq\\napt-get install -y -q --no-install-recommends \\\\\\n    nodejs\\nrm -rf /var/lib/apt/lists/*" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "bash -c '"'"'npm install -g bids-validator@0.19.8'"'"'" \
      } \
    }, \
    { \
      "name": "env", \
      "kwds": { \
        "FSLDIR": "/usr/share/fsl/5.0", \
        "FSLOUTPUTTYPE": "NIFTI_GZ", \
        "FSLMULTIFILEQUIT": "TRUE", \
        "POSSUMDIR": "/usr/share/fsl/5.0", \
        "LD_LIBRARY_PATH": "/usr/lib/fsl/5.0:", \
        "FSLTCLSH": "/usr/bin/tclsh", \
        "FSLWISH": "/usr/bin/wish" \
      } \
    }, \
    { \
      "name": "env", \
      "kwds": { \
        "OS": "Linux", \
        "FS_OVERRIDE": "0", \
        "FIX_VERTEX_AREA": "", \
        "SUBJECTS_DIR": "/opt/freesurfer/subjects", \
        "FSF_OUTPUT_FORMAT": "nii.gz", \
        "MNI_DIR": "/opt/freesurfer/mni", \
        "LOCAL_DIR": "/opt/freesurfer/local", \
        "FREESURFER_HOME": "/opt/freesurfer", \
        "FSFAST_HOME": "/opt/freesurfer/fsfast", \
        "MINC_BIN_DIR": "/opt/freesurfer/mni/bin", \
        "MINC_LIB_DIR": "/opt/freesurfer/mni/lib", \
        "MNI_DATAPATH": "/opt/freesurfer/mni/data", \
        "FMRI_ANALYSIS_DIR": "/opt/freesurfer/fsfast", \
        "PERL5LIB": "/opt/freesurfer/mni/share/perl5", \
        "MNI_PERL5LIB": "/opt/freesurfer/mni/share/perl5/", \
        "PATH": "/opt/miniconda-latest/bin:/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:/usr/lib/fsl/5.0:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin", \
        "PYTHONPATH": "" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "mkdir root/matlab && touch root/matlab/startup.m" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "mkdir /scratch" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "mkdir /local-scratch" \
      } \
    }, \
    { \
      "name": "copy", \
      "kwds": { \
        "source": [ \
          "run.py" \
        ], \
        "destination": "/run.py" \
      } \
    }, \
    { \
      "name": "run", \
      "kwds": { \
        "command": "chmod +x /run.py" \
      } \
    }, \
    { \
      "name": "copy", \
      "kwds": { \
        "source": [ \
          "version" \
        ], \
        "destination": "/version" \
      } \
    }, \
    { \
      "name": "entrypoint", \
      "kwds": { \
        "args": [ \
          "/neurodocker/startup.sh", \
          "/run.py" \
        ] \
      } \
    } \
  ] \
}' > /.reproenv.json
# End saving to specification to JSON.

%runscript
/neurodocker/startup.sh /run.py
