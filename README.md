# 🏎️ High-Speed Line Follower Robot (LFR)

A high-speed Line Follower Robot built using:

- Arduino Nano  
- Pololu QTR-8A Reflectance Sensor Array  
- TB6612FNG Dual Motor Driver  
- Differential drive mechanism  
- PD control with dynamic speed adjustment  

This project focuses on achieving stable and fast line tracking on a standard 20 mm black line using weighted sensor averaging and proportional-derivative control.

---

## 📌 Features

- 8-sensor weighted line position detection (0–7000 range)
- PD control for stable correction
- Dynamic speed control (faster on straights, slower in turns)
- Differential drive motor control
- Clean and modular motor driver implementation

---

## ⚙️ Hardware Configuration

### 🔋 Power
- 7.4V (2S) Li-ion / Li-Po battery recommended
- Battery → TB6612 VM
- Battery → Arduino VIN
- Common ground required between all components

### 👁 Sensors
- QTR-8A connected to A0–A7
- Sensor height: **3–4 mm from track**
- Recommended line thickness: **~20 mm**

### 🛞 Mechanical Recommendations
- Wheel spacing (center to center): **8–9 cm**
- Sensor placement: **3–4 cm ahead of wheel axis**
- Lightweight chassis (3mm acrylic recommended)

---

## 🧠 Control Strategy

### Line Position
The QTR-8A sensor array returns a weighted position value:

0 → 7000  

- 0 = line at extreme left  
- 3500 = centered  
- 7000 = line at extreme right  

### PD Control
Error is calculated as:

```
error = 3500 - position
```

Correction is applied using:

```
correction = Kp * error + Kd * derivative
```

### Dynamic Speed Control
Robot speed is reduced proportionally during sharp turns to improve stability and cornering performance.

---

## 📂 Code Usage

The source code is provided in a file named:

```
lfr_code.txt
```

To use it:

1. Copy the contents of `lfr_code.txt`
2. Paste into a new Arduino `.ino` sketch file
3. Upload to Arduino Nano

⚠️ Important:

The control parameters (Kp, Kd, speed limits, etc.) must be tuned according to:

- Motor RPM  
- Wheel diameter  
- Battery voltage  
- Track geometry  

Improper tuning may result in oscillation, instability, or line loss.

---

## 🔧 Tuning Parameters

The following values must be adjusted carefully:

- `Kp` – proportional gain  
- `Kd` – derivative gain  
- `maxStraightSpeed`  
- `minTurnSpeed`  
- Dynamic speed multiplier  

Suggested tuning process:

1. Increase base speed  
2. Increase Kp until oscillation begins  
3. Increase Kd to reduce oscillation  
4. Repeat until stable at desired speed  

---

## 🚀 Future Improvements

This project may be extended with advanced features such as:

- Line-loss detection and recovery logic  
- Multiple line detection handling  
- Junction detection  
- Intersection decision algorithms  
- Curvature prediction  
- Encoder-based closed-loop speed control  
- Higher PWM frequency optimization  
- Adaptive gain control  

These improvements can significantly enhance robustness and competition-level performance.

---

## 🎯 Applications

- Robotics competitions  
- High-speed line following challenges  
- Embedded systems experimentation  
- Control systems learning projects  

---

## 📜 License

This project is licensed under the MIT License.
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
