# ASR
Automatic Speech Recognition (ASR)

Automatic Speech Recognition (or speech-to-text) systems
transform speech into their corresponding text form,
typically in the form of a word sequence

website:
https://kaldi-asr.org/

# Kaldi Installation Steps For Beginners!


_Author : Suraj Durgesht_

1. Install Subversion

    sudo apt-get install subversion

2. Install Dependent Libraries
    sudo apt-get install libblas-*
    sudo apt-get install automake
    sudo apt-get install libtool-*
    sudo apt-get install libatlas-*
    sudo apt-get install zlib1g-dev
    sudo apt-get install g++-multilib
    sudo apt-get install flac

4. Installation via GitHub
      git clone https://github.com/kaldi-asr/kaldi.git
      cd kaldi/
      cat INSTALL
      cd tools/
      cat INSTALL
      make
      
5. Ceck out dependencies
    extras/check_dependencies.sh
    nproc
    
6. Istall a language modeling toolkit IRSTLM
	extras/install_irstlm.sh

7. Istructions in kaldi/src/INSTALL.
    cat INSTALL
    ./configure
    make depend -j 4
    make -j 4
