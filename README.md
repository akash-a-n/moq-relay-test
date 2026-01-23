# moq-relay-test
A tool for interop testing of MOQT relays

## Notes on installing on Ubuntu 24.04 LTS

Use the following steps to update system and install correct components
```
# Update system and install tools
apt update
apt upgrade
apt install build-essential git gcc g++ make libssl-dev m4 doxygen python3 libaio-dev

# Fetch repo
git clone https://github.com/akash-a-n/moq-relay-test.git -b feature/first-test

# Setup moxygen
cp moq-relay-test/moqt_implementation
./copy_moxygen.sh
cd moxygen
eval $(./build/fbcode_builder/getdeps.py env --src-dir moxygen:. moxygen)
./build/fbcode_builder/getdeps.py build moxygen

# Build test tool

# Upgrade to GCC 14 - to avoid internal compiler error observed with GCC 13
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install gcc-14 g++-14
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-14 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-14 100
sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30

cd ../../interop_test_framework/
./build_with_moxygen_env.sh
```