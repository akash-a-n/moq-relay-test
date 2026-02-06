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

# Compile test tools
cd ../../interop_test_framework/
./build_with_moxygen_env.sh
``` 