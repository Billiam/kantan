![kantan](http://i.imgur.com/TDiUkZo.png)

kantan is a way to make consistent 16-colour scheming simple. At its core is a tiny shell script that allows for templating of colour configuration files for whatever programs you use. It comes with templates for:

- vim
- Xresources (xterm et al.)
- iTerm 2
- st
- PuTTY
- Your pull request welcome!

kantan doesn't trash the ANSI colour codes, making it work with your console programs by default. Bright green appearing as dark grey really sucks, and you don't always have control of colours in situations like connecting to a server over ssh. This makes it perfect for users who run many console based programs or spend a lot of time in the terminal.

kantan depends on bash and awk. That's it. This means that you don't have to install ruby or python on a newly provisioned server just to build your colour schemes; kantan works out of the box.

kantan is inspired by [base16-builder](https://github.com/chriskempson/base16-builder) and derives some structure from it.

## Default Scheme

kantan comes with a modified version of base16's default scheme, modified to conform to the ANSI codes.

Palette (there's a template for this image, palette.svg):

![default scheme palette preview](http://i.imgur.com/LUOXy3V.png)

xterm on ArchLinux:

![default scheme xterm preview](http://i.imgur.com/m2YFQep.png)

vim in iTerm 2 on OS X:

![default scheme vim preview](http://i.imgur.com/DQjRvsW.png)


## Usage

To build all templates with the scheme `schemes/default`:

    $ ./kantan

To build all templates with a custom scheme:

    $ ./kantan /path/to/scheme/file


If you use a git repository for your configuration dotfiles (highly recommended), integrating kantan is extremely easy. Just add kantan as a submodule, and modify your Makefile to tell kantan to build its templates. For an example, you can take a look at my [dotfiles repository](https://github.com/pushrax/dotfiles). Otherwise, you can just run kantan directly and copy or link the files it generates.


## Scheme format

Schemes are just shell scripts that define the `hex[n]` variables. Take a look at the default scheme for an example. Note that although this is a 16-colour scheme, there is one extra colour to use as a background colour, which is at `hex[16]`.

## Templating

Templates are extremely simple. Just insert `${var}` anywhere in the template to have it replaced with the desired colour code. `var` can be one of:

- `hex[0-16]` - hex representation
- `rgb_r[0-16]`, `rgb_g[0-16]`, `rgb_b[0-16]` - RGB red green and blue decimal values (0-255), respectively
- `srgb_r[0-16]`, `srgb_g[0-16]`, `srgb_b[0-16]` - sRGB red green and blue floating point decimal values (0.0-1.0), respectively
- Any other environment variable that you set

So if colour 3 had hex value `123456` and you wanted `something=#123456` you could do `something=#${hex[3]}` (note the leading `#`).


