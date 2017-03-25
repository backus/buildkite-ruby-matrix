# Dockerized Ruby Matrix for Buildkite

This is a Dockerized buildkite setup I use for testing a few open source Ruby projects I maintain. It is a lot more work to get setup, but once it is working it makes building projects really fast. Here is an example from [rubocop-rspec](https://github.com/backus/rubocop-rspec):

![rubocop-rspec build][rubocop-rspec-screenshot]

That is a 22 second build that ran specs and rubocop on three different versions of Ruby!

This repository mainly exists for my projects so I don't have to copy and paste around this setup. If you do use it on your own project then let me know!

[rubocop-rspec-screenshot]: https://camo.githubusercontent.com/1bfbb45edcc7b966cf714b7de85948a4e9ed27ee/687474703a2f2f692e696d6775722e636f6d2f413359765a58782e706e67

## Security

If you do use this, you should add a buildstep via Buildkite's dashboard that looks like this but with your own GPG signature:

```bash
gpg --keyserver keyserver.ubuntu.com --recv 1B3C10C4

git_signature=$(git --no-pager show --quiet --pretty='%G?: %GS %GK' HEAD)
expected_signature="U: John Backus <johncbackus@gmail.com> 9A91898D0B0B2FBE"

if [[ "$git_signature" != "$expected_signature" ]]; then
  echo "Expected signature: $expected_signature"
  echo "Actual signature:   $git_signature"
  echo

  git diff --exit-code origin/master -- .gitmodules build .buildkite
fi
```

This example verifies that no one is modifying the build besides you. This way you can accept third party PRs without it being trivially easy to just start running random binaries on the CI. I definitely wouldn't guarantee that this makes using this CI setup safe, but the Docker container does provide some isolation and this script makes sure you don't change the container.
