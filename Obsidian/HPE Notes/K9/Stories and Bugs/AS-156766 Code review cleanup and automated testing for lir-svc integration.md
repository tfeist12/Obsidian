To Do:
- increase coverage
- task_runner test
- update init to pending, protobuf3 idioms -> Ask britt if he wants this done this story
- lir confluence grpc commands

install script to call from node

pl2 build script installs release locally _. spins up nginx 172.19.0.101

go cli tool to act as grpc client of lirService

look into monkey patching channel sends
waitgroup

no clean up after addrelease and get status tests

Get status then run tasks: 1676572695256059164
validate input then run tasks: 1676572781271064140

Issue has something to do with new Tasks
split task runner into its own package
go vet ./... since it'll complain about copying the proto objects. I think the solution there is to add a SendStatus method to Task that ensures a new lir.StatusItem is created and change the release processing to use pointers.

breaking task runner into its own packagemakes us unable to define UpdateTaskStatus as a receiver

in task reference to a function to call (either install release or test functions)