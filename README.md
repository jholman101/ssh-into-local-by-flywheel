# SSH into Local By Flywheel

I spend most of my time working on the command line on my Mac.  When working with [Local by Flywheel](https://local.getflywheel.com/), I find it frustrating to go to the Local by Flywheel app and click a drop-down to SSH into the machine.

Instead, I'd prefer a command I can type from the command line that would:

- Based on the directory I'm currently in, SSH into the correct docker container.
- Based on the directory I'm currently in, within the docker container change to the corresponding directory.

## SSH Script

The `sshlbf` (for SSH Local by Flywheel) does this task based on a file called `.dockerid` that needs to be manually created in the root directory for that particular site.  The `.dockerid` file should contain one line that has the container name for that site.

## Setup WP CLI from Host Machine

Much of my command line work that requires SSHing into the machine specifically involves using [WP CLI](http://wp-cli.org/). Thanks to work by [Morgan Estes](https://github.com/morganestes), I found I could add some configuration files to my local project that would allow me to use WP CLI from my Mac on the WordPress site running inside Local by Flywheel.

### How to Setup

To setup WP CLI to work from the host machine (your Mac), you need to add `wp-cli.local.yml` and `wp-cli.local.php` to your project root directory (i.e. next to `app/`, `conf/`, and `logs/`). I've added a helper script to this project to do just this.

On your host machine (your Mac), navigate to the root directory of your project.  When you run `ls` you should see

```
app     conf    logs
```

Then run the helper script in this project

```
$ wpcli-lbf-setup
```

Then you'll be prompted for the **Database host** and **Database port**, both of these values can be found in the Local by Flywheel interface under your Site > DATABASE settings.

Then you should see a Success message,

```
Successfully connected to http://example.test
```

where `example.test` will be replaced by your local site URL.

### Using WP CLI

Now from your host machine (your Mac) you can enter a WP CLI command and it will be executed in the Local by Flywheel guest website.

```
$ wp plugin list
```

### Troubleshooting

If the script shows a failure message, try the following:

- Confirm the site is running in Local
- Double-check the database host and port

## Credits

[Sal Ferrarello](https://salferrarello.com) / [@salcode](https://twitter.com/salcode)
