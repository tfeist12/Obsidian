localOSDClient -> localGrpcClient

sm should contain grpc client

grpc client
- osd on dsp side
- ippodd on ippod side

I need a way to determine within the etcd client 

newDSP calls newACT, sets the type and any other unique properties?

I need to create a new type called an act-pod this is going to be very similar to the dsp definied here. It swhould have all the same fields. The statemachine is even the same. I'm going to create a seperate type called an ippod. both dsp and ippod are an act-pod. The problem is that within the statemachine there will be states where we will need to know the type of the act-pod. How do i solve this issue

Make config an interface that is a part of the act base
Load config at the top level at creation time

ip pods ids should be the same 

osd-> grpc

Config
whoever is calling the getter 
define interface that contains getters

no ippod aversion label

