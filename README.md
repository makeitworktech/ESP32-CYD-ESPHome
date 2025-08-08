# Intro
This is a small repo to place my YAML files for the ESP32-CYD variants that I use.
Note that this project is heavily influienced by https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display, so huge shout-out to [@witnessmenow](https://github.com/witnessmenow) and [Jonny Bergdahl](https://github.com/jonnybergdahl) for all of their effort over there.

So far I have a few different variants of the CYD. For both of them I have created example code, and these YAML files are named respectively.

A lot of the information for these boards can be found either here [@witnessmenow](https://github.com/witnessmenow) or [LCDwiki](https://www.lcdwiki.com/Main_Page#ESP32_Display_Module).

I'm working on a YouTube video for this whole project, and I'll post a link here when done.

Thanks for reading!

Aaron

# Prerequisites
1. An ESP32 CYD. The best ones are the ones defined here
    - ESP32-E32R28T: https://www.lcdwiki.com/2.8inch_ESP32-32E_Display
    - ESP32-E32R35T: https://www.lcdwiki.com/3.5inch_ESP32-32E_Display
    - ESP32-E32R40T: https://www.lcdwiki.com/4.0inch_ESP32-32E_Display

    These can be found at the following links. Note they are affiliate links, so I'll get a commission at no additional cost to you if you order from here:
    - ESP32-E32R28T: https://amzn.to/46OfP66
    - ESP32-E32R35T: https://amzn.to/4ftn45G
    - ESP32-E32R40T: https://s.click.aliexpress.com/e/_omdyQJl

2. A Windows PC
3. Home Assistant & ESPHome


# Instructions (Windows PC)

1. Install Python on your PC. ESPHome requires Python, so if you don't have it already, download and install Python from www.python.org. Make sure to check the box that says "Add Python to PATH" during installation. Don’t skip this step, it’s important!
2. Once installed, we need to create a project folder where all of the ESPHome files will be stored. I created one on my C:\ Drive called “esphome-display”, but you pick your location. After that, open a Command Prompt terminal by pressing Win + R, typing cmd, and hitting Enter. In the Command Prompt, type pip install esphome and hit enter. This will install ESPHome. If you want to verify the installation, type esphome version in the command prompt window, and hit Enter. This should display the version of ESPHome that you just installed.
3. Now we want to flash the YAML file onto the ESP32-CYD, so you’ll need the file. Download the one that applies to your CYD from the ESPHome examples folder. Place it in the project folder that you created.
4. In that same folder you should create a “secrets.yaml” file. This will have a few things like a Home Assistant API key, a few passwords, and your wifi credentials. If you want, you can just download an example of the secrets file, but you’ll have to fill it out with your own information and save it in your project’s directory. One of the things it will have is an API Key, which has to be a hexadecimal, 32 character key. You can actually just ask ChatGPT to generate one for you, and then store it there in your secrets file.
5. Another thing you’ll need are some fonts for the display, so download them and put them into a new folder called “fonts” in your project directory.
6. Now, connect your CYD to your PC with a USB-C cable. If you’re using the 2.8” version that I’m using, it will only come with micro-USB. You’ll see a demo screen that comes on, which gives you an idea of how it can work, the touch sensitivity etc, but of course that’s gonna go bye-bye when we’re done with it.
7. Back in the command prompt window, you need to change the directory that it’s looking at to your project folder. To do this, type “cd <space>”, followed by the path of your project folder. I typed “cd <space> C:\esphome-display”. Then, you can compile the YAML file you downloaded by typing in “esphome run “ and then the name of the YAML file you downloaded.
8. The window will show the compile log, and once it’s done it will ask you if you want to flash it via USB or over the air. Choose USB by typing the option number 1, and press Enter. You should see your screen go dark for a few seconds, and then you should see a 12-button display! If not, check the command prompt window to see if there were any errors.
9. You can test out pressing the buttons to see the reaction in the CMD window, and if you’re not happy with the pressure required, you could change that in the YAML. The last three buttons are toggles, so their state will change when you press them. The actual icons will update based on the Home Assistant entity that they are linked to, so you'll have to modify that to suit your particular entity.
10. Once the ESP32 is flashed and connected to your Wi-Fi, it should automatically appear in Home Assistant under the integrations. When you click add, it will ask if you want to add it to Home Assistant, and then it will ask you for the and Encryption key. This is just the API Key you created earlier, so copy that from your secrets folder and paste it in there.
11. When you click Submit, it will ask you if you want to put the new device in an area, and then you can click Finish and it will take you to the device page. On this page you’ll see a list series of 12 Binary Sensors, labeled Button 1 through 12, and these will turn to an “On” state when you press one of the buttons. Try them out and make sure that they’re all working.
You’ll also have a light entity that controls the backlight of your LCD screen, so toggling that will toggle the screen on and off. Along with that is a light entity to control the onboard RGB LED!
12. One other thing to note, once added to Home Assistant, you need to head to the ESPHome integration by clicking the link to it in the device page, then click the gear icon for that device, and make sure you check “Allow the device to perform Home Assistant actions”. This is important for allowing any of the buttons to directly control an entity in Home Assistant.

# Customization
*Font*

The font section of the code allows you to specify a font, and then you can use it later in the display configuration. You can see that I’ve specified this Arimo Regular font twice – once at size 42, and once at size 14. For each font, you need to specify which characters, or “glyphs”, will be used later on. Specifying only some will save memory. I don’t currently use these two fonts on my display, but If I wanted I could change one of the buttons to have text, so having these predefined is nice. I’ll show you where you use the text later. The next font is the material design icon font, and it allows you to use material design icons kind of like images for your buttons. Once again, you have to specify the glyphs you plan to use. It’s easy enough to get these glyphs by going to materialdesignicons.com, searching for the icon you want, clicking on it, and then clicking copy glyph in the upper right corner. Then you can paste it into your code as needed. Since the glyphs for these don’t really show up properly in text editor, it’s a good idea to use comments to keep them organized like I’ve done here.

*Colors*

The next customization I want to show you is the colors section. Here we can define the color of the background, the color of each button, the color of the buttons when pressed, and the text color for each button. The colors are HEX colors, so you can use a hex color picker if you need to so you can get the exact color you want.

*Lights*

In the lights section, you can customize how you want the light entities for the LCD Backlight and RGB LED to be named. This RGB LED setup isn’t perfect, as the green is super bright and the red is really dim, so we don’t get perfect color mixing.
Binary Sensors
Similarly, in the binary sensors section you can change the names of the buttons as they will appear in Home Assistant. The last three buttons will be used to control a specific entity in Home Assistant, but I still have them exposed there as binary sensors, just in case.

*Text Sensors*

Speaking of those buttons, next we have three text sensors, which mirror the state of an entity in Home Assistant. These sensors then update the “checked” condition of the button we have tied that entity to, and set a different icon for the button based on the on and off states of the entity. We’ll cover how to change the color of the icon dynamically in the next section. I have three of these buttons though, one for my office ambient lights, one for my fan plug, and one for my main office light. 

*LVGL*

The next section is called LVGL, and that stands for "Light and Versatile Graphics Library" — it's an open-source graphics library designed for embedded systems like microcontrollers – in this case the ESP32. In the context of ESPHome, LVGL allows you to create interactive GUIs on devices with touchscreens and displays. What I’ve done with it here is just barely scratching the surface of what it’s capable of, and there is excellent documentation for LVGL in the ESPHome context that I’ve linked in the description if you want to customize further.
The first thing you’ll see is a theme section, and this is where we define the color of button icons that are pressed, checked, etc. This allows us to set the colors for all buttons, although we can override the theme with individual color assignments further down in this section. Using the theme is what allows us to dynamically change the icon color
In this next section we have defined 12 buttons in a grid. Beside the last three, each button has a background color, a pressed color, a text label, and a text color. Changing any of these color options up in the colors section will affect the properties as shown here. If you want to change the icon displayed, you need to first go up to the fonts and add the icon’s glyph and then you can change it down here.

