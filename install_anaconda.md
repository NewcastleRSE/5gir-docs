
# Install Anaconda


## On Ubuntu

Download and Install Anaconda on Ubuntu with the following bash code:

```bash
filename_installer=Anaconda3-2025.06-1-Linux-x86_64.sh

dirname_installer_local="$HOME"/Downloads
dirname_installer_remote=https://repo.anaconda.com/archive

dirname_installation="$HOME"/anaconda3

filename_installer_local="$dirname_installer_local"/"$filename_installer"

filename_installer_remote="$dirname_installer_remote"/"$filename_installer"

wget -P "$dirname_installer_local" "$filename_installer_remote"

bash "$filename_installer_local" -b -p "$dirname_installation"

source "$dirname_installation"/bin/activate
conda init --all
conda config --set auto_activate_base false
conda deactivate

source "$HOME"/.bashrc
```


### On Windows

Download and Install Anaconda on Windows with the following CMD code:

```CMD
set "filename_installer=Anaconda3-2025.06-1-Windows-x86_64.exe"

set "dirname_installer_local=%UserProfile%\Downloads"

set "dirname_installer_remote=https://repo.anaconda.com/archive"

set "dirname_installation=%UserProfile%\Anaconda3"

set "filename_installer_local=%dirname_installer_local%\%filename_installer%"

set "filename_installer_remote=%dirname_installer_remote%/%filename_installer%"

set "cwd=%cd%"

cd %dirname_installer_local%

curl -O %filename_installer_remote%

cd %cwd%

start /wait "" %filename_installer_local% /InstallationType=JustMe /AddToPath=0 /RegisterPython=0 /S /D=%dirname_installation%

%dirname_installation%\condabin\conda.bat activate
conda init --all
conda config --set auto_activate false
conda deactivate

```

### On Mac
TODO
