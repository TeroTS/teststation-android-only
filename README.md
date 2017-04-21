Provisioning script for Android-only Appium
-------------------------------------------

This is for OSX only !

prerequisites:

	pip: sudo easy_install pip

	ansible: sudo pip install ansible

Warning: Following Ansible command will override your ~/.bash_profile file !

Setup the environment:
	ansible-playbook --ask-become-pass setup_android.yml

Check the installation: appium-doctor --android

If the android build tools not installed => run: echo y | ./teststation/android-sdk/tools/android update sdk -u -a -t build-tools-25.0.1

start Python virtualenv: source ~/teststation/venv/bin/activate

Fix for Appium Python client issue (https://github.com/appium/python-client/issues/162):

pip uninstall selenium

pip install selenium==3.3.1

Get the tests: git clone https://github.com/TeroTS/AppiumDemo.git

Attach device (with developer options enabled)

Get device id: ./teststation/android-sdk/platform-tools/adb devices 

=> device id

Start Appium server: appium -p 4491 --default-capabilities '{"udid":"device id"}'

Create new resource file to ./AppiumDemo/mobiili_demo/resources/variables_{device name}.txt corresponding your device id and appium server port (4491)

cd ./AppiumDemo/mobiili_demo

pybot --variable PHONE_MODEL:{device name} mobile_demo_native_android.txt
