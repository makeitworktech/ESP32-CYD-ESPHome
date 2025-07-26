# Intro
This is a small repo to place my YAML files for the ESP32-CYD variants that I use.
Note that this project is heavily influienced by https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display, so huge shout-out to [@witnessmenow](https://github.com/witnessmenow) and [Jonny Bergdahl](https://github.com/jonnybergdahl) for all of their effort over there.

So far I have a few different variants of the CYD. For both of them I have created example code, and these YAML files are named respectively.

A lot of the information for these boards can be found either here [@witnessmenow](https://github.com/witnessmenow) or [LCDwiki](https://www.lcdwiki.com/Main_Page#ESP32_Display_Module).

I'm working on a YouTube video for this whole project, and I'll post a link here when done.

Thanks for reading!

Aaron

# Instructions (Windows PC)

1. Install Python on your PC. ESPHome requires Python, so if you don't have it already, download and install Python from www.python.org. Make sure to check the box that says "Add Python to PATH" during installation. Don’t skip this step, it’s important!
2. Once installed, we need to create a project folder where all of the ESPHome files will be stored. I created one on my C:\ Drive called “esphome-display”, but you pick your location. After that, open a Command Prompt terminal by pressing Win + R, typing cmd, and hitting Enter. In the Command Prompt, type pip install esphome and hit enter. This will install ESPHome. If you want to verify the installation, type esphome version in the command prompt window, and hit Enter. This should display the version of ESPHome that you just installed.
3. Now we want to flash the YAML file onto the ESP32-CYD, so you’ll need the file. Download the one that applies to your CYD from the ESPHome examples folder. Place it in the project folder that you created.
4. In that same folder you should create a “secrets.yaml” file. This will have a few things like a Home Assistant API key, a few passwords, and your wifi credentials. If you want, you can just download an example of the secrets file, but you’ll have to fill it out with your own information and save it in your project’s directory. One of the things it will have is an API Key, which has to be a hexadecimal, 32 character key. You can actually just ask ChatGPT to generate one for you, and then store it there in your secrets file.
5. Another thing you’ll need are some fonts for the display, so download them and put them into a new folder called “fonts” in your project directory.
6. Now, connect your CYD to your PC with a USB-C cable. If you’re using the 2.8” version that I’m using, it will only come with micro-USB. You’ll see a demo screen that comes on, which gives you an idea of how it can work, the touch sensitivity etc, but of course that’s gonna go bye-bye when we’re done with it.
7. Back in the command prompt window, you need to change the directory that it’s looking at to your project folder. To do this, type “cd <space>”, followed by the path of your project folder. I typed “cd <space> C:\esphome-display”. Then, you can compile the YAML file you downloaded by typing in “esphome run “ and then the name of the YAML file you downloaded.
8. The window will show the compile log, and once it’s done it will ask you if you want to flash it via USB or over the air. Choose USB by typing the option number 1, and press Enter. You should see your screen go dark for a few seconds, and then you should see a 12-button display! If not, check the command prompt window to see if there were any errors.
9. You can test out pressing the buttons to see the reaction in the CMD window, and if you’re not happy with the pressure required, you could change that in the YAML.
10. Once the ESP32 is flashed and connected to your Wi-Fi, it should automatically appear in Home Assistant under the integrations. When you click add, it will ask if you want to add it to Home Assistant, and then it will ask you for the and Encryption key. This is just the API Key you created earlier, so copy that from your secrets folder and paste it in there.
11. When you click Submit, it will ask you if you want to put the new device in an area, and then you can click Finish and it will take you to the device page. On this page you’ll see a list series of 12 Binary Sensors, labeled Button 1 through 12, and these will turn to an “On” state when you press one of the buttons. Try them out and make sure that they’re all working.
You’ll also have a light entity that controls the backlight of your LCD screen, so toggling that will toggle the screen on and off.


