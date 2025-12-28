# VSD_WORKSHOP
this repo is tracking the progress made in the VSD certification workshop for OpenLane flow

# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
Commands to invoke the OpenLANE flow and perform synthesis
# code
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a ( i have tapped in a previous design as runs was broken )
                       (we can use -tap argument to return to any past run, instead of creating a new one)
run_synthesis

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/163999aa-5eff-4b05-bfdb-f9cc80d82e4c" />
Running synthesis
# code
run_synthesis
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/b755ddbb-1c20-4310-832d-f761440c4cf5" />
synthesis was runn successfully

Calculating the Flop Ratio
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/c528c002-c9b0-4ba4-9b2b-5bbfc017b249" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/76ec1c1d-96f8-406f-a298-58a0b2dfd840" />
Calculation of Flop Ratio and DFF % from synthesis statistics report file
Flop Ratio = 1613 / 14876 = 0.108429685
Percentage of DFF's = 0.108429685 ∗ 100 = 10.84296854   % 

# Section 2 - Good floorplan vs bad floorplan and introduction to library cells 
# 1.Running the floorplan
# code
run_floorplan

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/441e4a46-3a9c-461b-8d7d-d780a51a0dce" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/efe86861-9c34-4ccf-a51d-2a41646b1c76" />
due to issues with run_floorplan, we will split it into 3 commands
# code
init_floorplan
place_io
tap_decap_or
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/344b017d-81be-49e8-ad9a-4d2ce45efa2e" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/70fb841e-0032-4b6b-9bad-f1a88b7aa128" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/74fd47ef-470f-40a5-80f6-78204f390828" />

now we have finished with the floorplan
# 2. Calculate the die area in microns from the values in floorplan def.
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/c572f6c7-0d30-41ad-848e-61932f556365" />
this is the image of the floorplan def file
According to floorplan def

Unit Distance: 1 µm
Die Dimensions (in unit distance):
Width = 660,685 − 0 = 660,685
Height = 671,405 − 0 = 671,405
Convert to microns (using 1 unit = 1,000 µm):
Die Width = 660,685 ÷ 1,000 = 660.685 µm
Die Height = 671,405 ÷ 1,000 = 671.405 µm
Die Area (µm²):
Area=660.685×671.405=443,587.212425 µm²
Summary: The die measures 660.685 µm × 671.405 µm, with a total area of 443,587.21 µm².

# 3. Load generated floorplan def in magic tool and explore the floorplan.
# code
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/27-12_08-1/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/da06bd3a-72d3-4333-aa48-2b9885fb2835" />
image of the floorplan uploaded in magic tool
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/2a189d6a-3441-4cee-926c-b1ad369ef9df" />
showing the equidistant placement of the ports
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/b8270e29-e624-4389-a5ec-a3126fbb39e5" />
decap and tap cells, note the tap cells are placed diagnoally equidistant from each other
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/13477920-96d4-4b60-8603-f05df20190da" />
image showing the unplaced standard cells

# 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
# code
run_placement
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/52380bfe-a4b5-4e7c-9b68-d197068c0357" />
running the placement
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/e2742e7e-9cf9-4746-8853-acfc57629e7a" />
placement has completed

# 5. Load generated placement def in magic tool and explore the placement.
# code
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/27-12_08-1/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/2a113872-2226-4130-8cef-5fef75ad1e01" />
the cell after placement, as seen in magic tool
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/b406719d-3a12-48e3-829f-776fcfcc3854" />
all standard cells are legally placed

# Section 3 - Design library cell using Magic Layout and ngspice characterization
# 1. Clone custom inverter standard cell design from github repository
# code
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
magic -T sky130A.tech sky130_inv.mag &

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/ca7eb1cb-255b-4c3d-8f26-e2f34a6ec84c" />
here we are able to see the cloned design, and are openign it in magic 
(the git clone command has not been run as this step was done before hand)
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/41bad2d2-277f-49f7-9c80-1fd80e3c76f3" />
the invertor design as seen in the magic tool
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/069cb3bb-795f-45f1-ba99-af45c1e5a7ec" />
the nmos and pmos are clearly identified with the code 
# code
select area //( after selecting the design )
what

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/fac02612-8714-4ec1-8524-69a6bc255ca8" />
Y connected to drain of both the mosfets
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/80c7b9ba-4639-4b9d-a665-5292b4efadd4" />
PMOS source is conencted to vdd or Vpwr
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/83691aed-8e1b-4917-8b55-da81b6c250c8" />
NMOS source conencted to ground here VGND
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/3dbcc476-a527-416e-a887-ba112be88a0d" />
DRC error clearly visible on deleting a section of the poly for gate terminal
 # 3. Spice extraction of inverter in magic.
 # code
 extract all
 ext2spice cthresh 0 rthresh 0 //this is done to tolerate no RC, ie include all the parasitics
 ext2spice

 <img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/d83cb6a7-275a-43ca-adfa-e25e5b31b57f" />
the model is extracted to spice file

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/2313dce6-6a8c-4f38-b9b1-aa26a2a211c6" />
the created spice file 

# 4. Editing the spice model file for analysis through simulation.
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/ad6dd1fb-30c5-487e-8352-733adcf0014e" />
unit distance of layout is 0.01






































till now we have done all the steps before the sta analysis and now we will repleae the cells with those of higher drive strength so that we can reduce the deley
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/8f7cbb00-4b3f-4857-8625-3c56bcd5628b" />

the or gate that we are going to replace with higher drive strength one as it has 4 as fanout but less drive strength
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/0f8dfc24-821a-4f35-991c-77eebc1a24f2" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/9d0c70c5-2fea-4aa8-b7a1-dfce98aac1e2" />
<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/f57c0516-1dc9-4992-8131-5ad7f7fcc451" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/a79a61a1-b20f-48e5-869e-52fc81c286fe" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/258a9fb4-cb4b-45f7-a039-845c3d352974" />
clearly the slew improved from -23.9 to -23.5


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/1511949c-f07f-4579-8bf1-03ca73c3fca2" />
this is the second OR gate that has significant delay and we will replace it with higher drive strength

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/f39e9c27-6595-408e-ac03-651d02228293" />
replacing the next cell, but rerun the analysis I forgot to put digits argument

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/ac2c0c98-9382-4024-8ac3-f39adf695b3b" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/49925b0b-8893-47e6-8daf-acf595af53a8" />
cleary slew reducsed to -23.5049 from -23.5092

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/93ab5eab-708b-444d-9240-af543c763b6c" />
screenshot of the replaced cell 14510 with the new cell of higher drive strength

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/63b66d63-770e-4f0e-844d-bed93088a4e1" />
another OR gate with excessive delay, replacing it with or4_4


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/b2b02512-be74-4bf0-ad7c-e473fa2f87dc" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/a9e56385-18f5-48ff-86c5-f024b0e8c524" />


slew has further reduced from -23.5049 to -22.9860

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/7966c56e-73e7-40c5-abb0-03086efe07ca" />

replacing another delayed OR gate with upsized gate

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/608ea1db-340c-40d3-9e40-886774b5a4d2" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/57bb87b5-c518-48b2-80e7-52f8b275554b" />
skew further reduced to -22.6173

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/b40bfe3a-a844-499b-9f90-a11bde906d95" />

making a copy of the netlist before chanigng that with the changed netlist after having perforrmed sta analysis using openSTA

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/7d22da6f-3efb-4920-a78c-207df919ab51" />
here we have used the write verilog command to write the new netlist into the synthesis file in the runs directory

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/8f9ca5f4-05df-40f4-9dfe-7a0c58c464f8" />


verifying that the changed instance is clearly visible in the new netlist that is created and uploaded


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/0cd2167a-f096-427a-8612-184a4bca20c5" />

clearly seen, post placement, the new netlist lead to a decrease in slack but increase in area


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/39aaf324-4159-4fd1-8eb5-d9d61dbb0fbd" />

image showing successful CTS run

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/78bcafc6-90df-4d5f-aaa7-e3a8a389bb24" />
screenshot of creationg of DB for the purpose of using openSTA inside openroad

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/f609f9a1-d9a3-4d42-9f84-2c244acb54f0" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/f94acf03-5fd0-4df7-b796-12646abce673" />

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/c1ab9837-dbc1-4857-bb37-190e07fbe7c8" />
these are the images after running the cts ( report checks )

later learnt, this analysis is wronga s we have included the min max libraries for the analysis but tritonCTS has optimised for the typical corner


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/1c33f767-2970-448f-900c-586af57af339" />

this is re run on openroad timing analysis but this time uploading only typical corner

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/0754a354-b20b-4999-aded-2d661a7bd24d" />
still hold violation exists


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/660d8fde-18aa-4a30-a03c-e5f7c90cc223" />
setup condition has been met, wrongly shown previously due to faulty assessment


Now we will edit the buffer list and see its effects on the timing analysis


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/40a745bf-5187-4d66-8c15-bbdb17a8b97d" />


here we are changing the bufferlist


<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/0a0d66e4-628b-4e27-91d4-519a9136a6e0" />
finished rerunning cts with new buffer list

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/5e96d004-2a3b-4e75-ae3e-b613d769b5c7" />
again running timing analysis in openroad

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/65e987d1-9d83-483a-87e6-86c8122b3e13" />
hold time violation resolved due to the use of larger buffers

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/311aa3f4-fea6-4b15-b8ce-55ba9ab1519b" />
setup time margin improved with the use of larger buffers

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/f1ae6aa1-88e6-42fe-b134-27a779f33b1f" />
 verifying the setup and hold clock skews

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/ac71d322-6a53-42e7-aef7-1fee43904813" />
here we are reinserting the buffer1 in the buffer list
now we will run gen_pdn command to generate power distribution network

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/4991333b-3e41-4a4f-837f-39809ee6e860" />
the new def file containing the layout has been created in the floorplan folder

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/80dc7e02-90c3-43c6-8bbe-197be2741876" />

now we will start running the routing at the default configuration to save time

<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/627d8670-3103-42bb-a6e3-3fda23080221" />

routing was finished with no DRC violations
















