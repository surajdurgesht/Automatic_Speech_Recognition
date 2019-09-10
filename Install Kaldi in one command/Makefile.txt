# Use a prebuild Kaldi to omit the installation
KALDI :=


pipi() {
    REQ_FILE=Requirements.txt
    TMP_FILE=/tmp/tmp_req.txt
    pip install "$@"

    if [ $? -eq 0 ] && [ -f "${REQ_FILE}" ]
    then
        FREEZE="$(pip freeze)"
        for arg in "$@"
        do
            if [[ $arg != -* ]]; then
                # sed -i "/^$arg[=<>]/dI" $REQ_FILE  # Should work on newer sed versions
                grep -vi "$arg[=<>]" $REQ_FILE > $TMP_FILE  
		        mv $TMP_FILE $REQ_FILE
                echo "$FREEZE" | grep -i "^$arg[=<>]" >> $REQ_FILE
            fi
        done
    fi
}


ifneq ($(strip $(KALDI)),)
kaldi.done:
	ln -s $(abspath $(KALDI)) kaldi
	touch kaldi.done
else
kaldi.done:
	test -d kaldi || git clone https://github.com/kaldi-asr/kaldi.git
	cd kaldi/tools; $(MAKE) all
	cd kaldi/src; ./configure --shared --use-cuda=no; $(MAKE) depend; $(MAKE) all
	touch kaldi.done
endif


