# voipwardialer
A Voip Wardialer for the phreaking of 2020

# Intro
This project aims to provide a modern voip wardialing free software.

It's meant for seasoned and young hackers willing to play with the old good telephony system from the comfort of their notebook.

It try to overcome the telecommunication related carrier over compressed audio codec used in VoIP, by trying to negotiate carriers with speed of 300bit/s 600bit/s 1200/bit. 

The software is meant also to be as simple and easy software voip dialer with modem deteciton, modem modulation/demodulation that finally let you interact with the remote system trough terminal emulation.

Most of the project that went working on something like this gave up due to the many complexity across telecommunication and not ready software modem stack that can be easily used and integrated.

VoIP Wardialer need to first solve this nifty problem, reaching a working sofware modem (DSP) that you can use and provide you an I/O with a remote system terminal from within your application.

# Archicture
VoIP Wardialer made up of two component:
- The VoIP Wardialer
- The Modem Server

The VoIP Wardialer is a Python 3 application that use [PJSUA](https://www.pjsip.org/pjsua.htm) VoIP Stack with [Python 3 binding](https://github.com/mgwilliams/python3-pjsip).

It does call the target phone number,  detect if there's a modem answering, negotiate modem carrier with a Remote Modem Server, provide then I/O of the remote system terminal dumping it's content into a file or to standard output.

To connect the audio flow coming from the called phone number to the Modem DSP running on Modem Server:

1. VoIP Wardialer starts another SIP VoIP call to a pre-configured Asterisk (running in localhost)
2. VoIP Wardialer setup a conference bridge between the two calls (One to remote system, one to local Asterisk)
3. Asterisk-Softmodem is used by Asterisk in the Modem Server negotiate the modem carrier
4. Asterisk-Softmodem provide the I/O of the remote system termina connecting via TCP a VoIP Wardialer listener

It's a neat workflow of data going around that may require a schema.

# Try it out
The MVP is meant to be ready for experiment and contribute in the making of VoIP Wardialer software

To use VoIP Wardialer you need at least:
* A Linux Debian machine
* A SIP account at VoIP Provider or your own SIP Server
* A phone number to call where modem answer

To install it we first need to build the PJSUA VoIP stack, that will then be used as telephony engine:
TODO: Describe how to install PJSUA


TODO: How to we deliver Asterisk? By a docker image or by apt-get install asterisk + copy configuration files in /etc/asterisk?

Tech specs are:
* Python 3 code
* PJSUA library for SIP/VoIP dialing and Conference Bridging
* Remote Modem DSP Server (An Asterisk [Asterisk-Softmodem](https://github.com/irrelevantdotcom/asterisk-Softmodem))


# Roadmap
* Experiment to make DSP properly working
  * Make DSP Modem (hooked to Asterisk) working properly and consistenly (this is the most important hit of the project!)
  * Integrate a C native code software modem (Linmodem? Fisher-Modem?)
  * Try Asterisk BTX Modem?
* Modem Detection trough Audio Sample Frequency Analysis (like [WarVox Classifiers](https://github.com/rapid7/warvox/blob/master/config/classifiers/01.default.rb)
* Modem Server Configuration Generation
* Remote Modem Server (to run it on another machine)
* Scanning functionalities 
  * Range generation
  * Session resumption
  * Logging of carrier and output of those carriers
* Multi channel parallel dialing
* Provide interactive terminal emulation connector (ptsy/tty for use with Minicom or other terminal emulation sw/lib)


# Resources
Making a project like this implies a lot of complexity

## Software Modem
Most of them with some specific limit or integration complexity
* [Asterisk-Softmodem](https://github.com/proquar/asterisk-Softmodem)
* [Asterisk-Softmodem](https://github.com/irrelevantdotcom/asterisk-Softmodem) fork with parity bit improvements
* [Asterisk Btx Modem](https://github.com/Casandro/btx_modem)
* [Fisher Modem](https://github.com/randyrossi/fisher-modem)
* [Linux Softmodem](https://bellard.org/linmodem/)

# Example Modem to call around the world for testing
TODO: List 10-15 modem to call that works across various countries to make experiments