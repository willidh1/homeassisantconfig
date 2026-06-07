# Google Nest Camera Control Setup Guide

## 📋 Overview
This guide will help you set up camera on/off controls for your Google Nest cameras in Home Assistant.

## 🔍 Step 1: Find Your Camera Entity IDs

Before you can use the scripts and automations, you need to identify your camera entity IDs.

### Method 1: Using Developer Tools
1. In Home Assistant, go to **Developer Tools** → **States**
2. In the search box, type `camera` or `nest`
3. Look for entities that look like:
   - `camera.front_door`
   - `camera.back_garden`
   - `switch.front_door_camera`
   - `switch.back_garden_camera`
4. Write down all your camera entity IDs

### Method 2: Using Devices & Services
1. Go to **Settings** → **Devices & Services**
2. Find and click on **Google Nest**
3. Click on each camera device
4. Look for the entity IDs listed (they start with `camera.` or `switch.`)

### Example Entity IDs
Your cameras might have entity IDs like:
- `switch.front_door_camera`
- `switch.back_garden_camera`
- `switch.driveway_camera`
- `camera.front_door`
- `camera.back_garden`

**Note:** The `switch.` entities control whether the camera is on/off, while `camera.` entities show the video feed.

## 🔧 Step 2: Update Configuration Files

### Update scripts.yaml
1. Open `scripts.yaml`
2. Find all instances of `CAMERA_NAME_1`, `CAMERA_NAME_2`, `CAMERA_NAME_3`
3. Replace them with your actual camera switch entity IDs

**Example:**
```yaml
# Before:
- switch.CAMERA_NAME_1
- switch.CAMERA_NAME_2

# After:
- switch.front_door_camera
- switch.back_garden_camera
```

### Update automations.yaml
1. Open `automations.yaml`
2. Scroll to the bottom where the camera automations are
3. Replace all `CAMERA_NAME_1`, `CAMERA_NAME_2`, `CAMERA_NAME_3` with your actual entity IDs
4. For the NFC tag automation, replace `REPLACE_WITH_YOUR_TAG_ID` with your actual tag ID (or delete that automation if you don't use NFC tags)

## 📱 Step 3: Test the Configuration

### Check Configuration
1. In Home Assistant, go to **Developer Tools** → **YAML**
2. Click **CHECK CONFIGURATION**
3. If there are errors, fix them before proceeding

### Restart Home Assistant
1. Go to **Settings** → **System** → **Restart**
2. Click **RESTART** and wait for Home Assistant to come back online

## 🎮 Step 4: Test the Scripts

1. Go to **Developer Tools** → **Services**
2. Search for `script.cameras_on`
3. Click **CALL SERVICE** to test turning cameras on
4. Search for `script.cameras_off`
5. Click **CALL SERVICE** to test turning cameras off

If the scripts work, your cameras should turn on/off!

## 📊 Step 5: Add Dashboard Controls

Use the examples in `camera_dashboard_example.yaml` to add camera controls to your dashboard:

1. Go to your Home Assistant dashboard
2. Click the three dots (⋮) in the top right
3. Click **Edit Dashboard**
4. Click **+ ADD CARD**
5. Choose **Manual** at the bottom
6. Copy one of the examples from `camera_dashboard_example.yaml`
7. Replace the placeholder entity IDs with your actual camera entity IDs
8. Click **SAVE**

## 🤖 Available Automations

The following automations have been added:

1. **Cameras ON when everyone leaves home** - Turns cameras on when both you and Eden leave
2. **Cameras OFF when someone arrives home** - Turns cameras off when either of you arrives
3. **Cameras ON at night (11 PM)** - Automatic overnight security
4. **Cameras OFF in morning (7 AM)** - Turns off if someone is home
5. **Toggle cameras with NFC tag** - Quick toggle with an NFC tag

You can enable/disable these automations in **Settings** → **Automations & Scenes**.

## 🎯 Available Scripts

The following scripts are available:

- `script.cameras_on` - Turn all cameras on (silent)
- `script.cameras_off` - Turn all cameras off (silent)
- `script.cameras_on_notify` - Turn cameras on with phone notification
- `script.cameras_off_notify` - Turn cameras off with phone notification
- `script.toggle_front_camera` - Toggle individual camera (example)

## 🔧 Customization Tips

### Change Automation Times
Edit the time triggers in `automations.yaml`:
```yaml
triggers:
- trigger: time
  at: '23:00:00'  # Change this to your preferred time
```

### Add More Cameras
Simply add more entity IDs to the lists in scripts and automations:
```yaml
entity_id:
  - switch.front_door_camera
  - switch.back_garden_camera
  - switch.driveway_camera
  - switch.garage_camera  # Add new camera here
```

### Change Notification Recipients
Update the notification service in scripts:
```yaml
- service: notify.mobile_app_pixel_8  # Change to your device
```

## ❓ Troubleshooting

### Cameras Don't Turn On/Off
- Verify your entity IDs are correct in Developer Tools → States
- Check that the Google Nest integration is working properly
- Ensure your cameras support on/off control (some models may not)

### Automations Don't Trigger
- Check automation conditions are met
- Verify device tracker entities are working (check in Developer Tools → States)
- Look at **Settings** → **System** → **Logs** for errors

### Scripts Not Appearing
- Ensure you restarted Home Assistant after editing `scripts.yaml`
- Check for YAML syntax errors in Developer Tools → YAML

## 📞 Need Help?

If you need to find your camera entity IDs:
1. Take a screenshot of Developer Tools → States (filtered by "camera" or "nest")
2. Share the entity IDs you find
3. I can help you update the configuration files with the correct IDs

## 🎉 You're All Set!

Once you've replaced the placeholder entity IDs with your actual camera entity IDs, your camera controls will be fully functional!