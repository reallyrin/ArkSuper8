import tkinter as tk
import cv2
import numpy as np
import threading
import time

class ThermalPrinterGUI:
def __init__(self, master):
self.master = master
self.recording = False

self.start_stop_button = tk.Button(master, text="Record", command=self.toggle_recording)
self.start_stop_button.pack()

self.print_button = tk.Button(master, text="Print", command=self.print_video)
self.print_button.pack()

def toggle_recording(self):
if self.recording:
self.recording = False
print("Record")
else:
self.recording = True
print("Record")
threading.Thread(target=self.record_video).start()

def record_video(self):
cap = cv2.VideoCapture(0)
while self.recording:
ret, frame = cap.read()
if ret:
cv2.imshow('Recording', frame)
if cv2.waitKey(100) & 0xFF == ord('q'):
break
cap.release()
cv2.destroyAllWindows()

def print_video(self):
cap = cv2.VideoCapture(0)
printer = open('/dev/usb/lp0', 'wb')
while True:
ret, frame = cap.read()
if ret:
resized_frame = cv2.resize(frame, (384, 288))
gray_frame = cv2.cvtColor(resized_frame, cv2.COLOR_BGR2GRAY)
_, dithered_frame = cv2.threshold(gray_frame, 200, 255, cv2.THRESH_BINARY)
dithere_frame = np.packbits(dithered_frame)
printer.write(dithered_frame)
time.sleep(0.1)
cap.release()
printer.close()

root = tk.Tk()
app = ThermalPrinterGUI(root)
root.mainloop()
