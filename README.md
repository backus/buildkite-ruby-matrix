# Dockerized Ruby Matrix for Buildkite

This is a Dockerized buildkite setup I use for testing a few open source Ruby projects I maintain. It is a lot more work to get setup, but once it is working it makes building projects really fast. Here is an example from [rubocop-rspec](https://github.com/backus/rubocop-rspec):

![rubocop-rspec build][rubocop-rspec-screenshot]

That is a 22 second build that ran specs and rubocop on three different versions of Ruby!

This repository mainly exists for my projects so I don't have to copy and paste around this setup. If you do use it on your own project then let me know!

[rubocop-rspec-screenshot]: https://camo.githubusercontent.com/1bfbb45edcc7b966cf714b7de85948a4e9ed27ee/687474703a2f2f692e696d6775722e636f6d2f413359765a58782e706e67

