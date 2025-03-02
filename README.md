# Windows 3.11 Starfield Screensaver Recreation


Recreate the classic Windows 3.11 starfield screensaver using Python and Pygame. This project simulates stars moving in a 3D perspective with dynamic brightness and optional color effects.

## Installation
  
1. **Clone the repository**:

   ```bash

   git clone https://github.com/Madoxx21/Win-3.11-ScreenSaver.git

   ```


2. **Set up a virtual environment** (recommended):

   ```bash

   python -m venv venv

   venv\Scripts\activate

   ```

3. **Install dependencies**:

   ```bash

   pip install -r requirements.txt

   ```

## Implementation Details

###  Data Structures

#### number_of_stars
- number of stars is not a such a strict choice , so based on my taste, I decided to go with 1000 stars

#### speed
- speed equal to 0.4 gives plausible outcome with my feature - scale_on_approach (will be described later)

#### stars
- I decided to store each star as a List inside an another list - stars, because for each star we have only 4 properties, so we would be able to access them in O(1) time complexity and we don't need to use dictionaries, because 4 properties is not so much to remember, and also using dictionaries is not so memory efficient (compare to lists). So, lists would be more conveneint in this case (also entire notebook is already structured to use lists).
#### Describtion of properties for each star
  - `x, y`: 2D coordinates adjusted for perspective

  - `z`: Simulated depth (starts at 256)

  - `color`: Brightness (0-255) or RGB tuple

  ```python

number_of_stars = 1000

speed = 0.4

stars = []

  ```

### New star implementation

```python
 x = random.randint(-screen_width // 2, screen_width // 2)
 y = random.randint(-screen_height // 2, screen_height // 2)
```

  - Because the origin of coordinates in Pygame is at the top-left corner of the window, we must set the range correctly. In my case x, y varies from -540 to 540.

### Move and Check implementation

  `move_and_check` function updates the position and brightness of a star. It modifies the star's coordinates, adjusts its brightness, and regenerates it if necessary. 

### Extra: Scale on approach feature implementation

I decided to add extra feature called `scale_on_approach`. This function calculates the **apparent size** of a star based on its `z`-depth, making it appear larger as it moves closer. This creates the effect that the viewer (in the animation) is flying through the stars
### Draw star implementation

`draw_star` function **renders a star** on the screen based on its position, depth, and brightness. It changes the coordinates to match the window coordinate system.
  ```python
    x = (star[0] * 256) // star[2] + screen_width//2
    y = (star[1] * 256) // star[2] + screen_height//2
```

Moreover, this function uses my extra feature in order to display scaled size of stars

### Pygame starfield simulation

  This script initializes a **Pygame starfield simulation**, where **1,000 stars** move forward at a set speed. It continuously updates their positions, regenerates them if they go off-screen, and draws them as glowing circles. The loop runs until the user quits, creating a dynamic starry background. 

## Conclusion

This starfield simulation in Pygame creates a visually dynamic effect by simulating stars moving toward the viewer. Using perspective projection, brightness adjustments, and scaling based on depth, the program effectively mimics the appearance of stars in motion. Each star is updated frame by frame, ensuring a smooth, immersive experience.