# darkphoton_highmass

#SW
#MG5_aMC_v2_9_16
#MadAnalysis5_v1.9.60.tgz


Step 1 Install Madgraph 

```
source /cvmfs/sft.cern.ch/lcg/views/LCG_99/x86_64-centos7-gcc8-dbg//setup.sh
#source /cvmfs/sft.cern.ch/lcg/views/LCG_99/x86_64-centos7-gcc8-dbg//setup.csh

git clone https://github.com/violatingcp/darkphoton_highmass.git
cd darkphoton_highmass
export DPHOME=$PWD

cd $MADGRAPH_BASE 
./bin/mg5_aMC
install pythia8
install Delphes
exit
export PYTHIA8DATA="/uscms_data/d3/pharris/Prod/tmp2/MG5_aMC_v2_9_16/HEPTools/pythia8/share/Pythia8/xmldoc/"

cp $DPHOME/generate_base.txt .
cp $DPHOME/launch_dpscan.txt .
cp -r $DPHOME/HAHM_variableMW_v3_UFO models
cd models/HAHM_variableMW_v3_UFO
python write_param_card.py
cd -		    
./bin/mg5_aMC generate_base.txt
./bin/mg5_aMC launch_dpscan.txt
```

Step 2 Install Mad Analysis

```
cd $MA5_BASE
cp $DPHOME/delphes_card_cms_exo_20_004.tcl tools/PAD/Input/Cards/
cp $DPHOME/madnalysis.txt .
./bin/ma5 -R madnalysis.txt
```

Step 3 translate limit for epsilon of 0.01 to coupling epsilon by noting it scales as sqrt(mu) (see notebook)
