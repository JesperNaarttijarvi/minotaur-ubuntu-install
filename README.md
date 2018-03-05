# Minotaur ubuntu installer

## Prerequierments

- Nvidia driver > 387.26
- Cuda driver > 9.0
- Git (used for git clone)

## Overview

From a clean ubuntu install, this will install:

- Dependencies (gcc-5, libcurl4-openssl-dev, libssl-dev, libjansson-dev, automake, autotools-dev build-essential)
- Python requierments (python-setuptools, python-dev build-essential)
- Minotaur
- gpustatd
- Excavataur
and miners: excavator, ccminer, ccminer2 and ethminer.

This installation will also set up Xorg file with all gpus appended to Display 0

All will run on startup. You should adjust the configuration to your needs.

## Usage

````
1. Log in as root
2. go to /~ (cd /root)
3. git clone https://github.com/JesperNaarttijarvi/minotaur-ubuntu-install.git
4. cd minotaur-install-ubuntu
5. ansible-playbook -i 'localhost,' -c local playbooks/server.yml


````

Then reboot the system.

This will deploy:

- xorg with appropriate config for all Nvidia devices on the system
- a "miner" user to run the applications with
- gpustatd - starting on boot
- excavator - starting on boot
- excavataur - starting on boot
- ccminer
- ccminer2
- ethminer
- gs display for minotaur - starting on boot

minotaur itself will not start on boot but you can change this by uncommenting
the line for it in /etc/rc.local. First you will probably want to do some
calibration though - see the README in the minotaur project for details.

All of the startup applications will run in screen sessions owned by the miner
user. You should run minotaur as the miner user, eg:

````
sudo su miner
````

then you can see the list of screen sessions with:

````
screen -list
````

jump into one with -r, eg to see the gs display:

````
screen -r gs
````

to exit from a screen session press ctrl-a and then d.

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
