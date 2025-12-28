<img width="1920" height="1075" alt="image" src="https://github.com/user-attachments/assets/a48a31c0-6bee-47c5-89f2-dc216e5703c2" /># VSD_WORKSHOP
this repo is tracking the progress made in the VSD certification workshop for OpenLane flow

lecture 65 onwards, till now we have done all the steps before the sta analysis and now we will repleae the cells with those of higher drive strength so that we can reduce the deley
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
















