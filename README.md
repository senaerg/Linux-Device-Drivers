# Linux-Device-Drivers
Linux device driver development project for platform drivers
# Build and Install

# Clone the repo
git clone https://github.com/senaergullu/linux-device-driver-1

cd custom_drivers/004_pcd_platform_driver

# Build the module
make

# Load with custom parameters
sudo insmod pcd_platform_driver.ko count=4 size=1024

# Verify
ls -l /dev/pcd*
dmesg | tail -20


# Test the Driver
# Test basic operations
echo "Hello PCD" > /dev/pcd0
cat /dev/pcd0

# IOCTL test program (separate test app needed)
./ioctl_test /dev/pcd0

# Testing the Commands
# 1. Load driver
sudo insmod pcd_platform_driver.ko count=3

# 2. Check devices
ls -l /dev/pcd*

# 3. Test read/write
echo "test data" > /dev/pcd0
dd if=/dev/pcd0 of=/tmp/test.out bs=1024 count=1

# 4. Check kernel logs
dmesg | grep PCD

# 5. Unload cleanly
sudo rmmod pcd_platform_driver
