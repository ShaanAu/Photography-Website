# AutoPhugo

AutoPhugo [ˌɔtoʊˈfjuːgəʊ] is a gallery/photoblog theme for Hugo that's a little more automatic than [Phugo](https://github.com/kc0bfv/phugo/).  It is a port of HTML5 UP [Multiverse template](https://html5up.net/multiverse).  Phugo was originally created by Aerohub, Pavel Kanyshev.

Preview at <https://kc0bfv.github.io/autophugo>

## Features

- Fully Responsive
- HTML5 + CSS3
- FontAwesome Icons
- Multi-level Albums Support
- Google Analytics
- Basic Breadcrumbs
- Contact Form
- Automated Image Scaling

## Recent Change

**PLEASE NOTE**

On 19 Dec 2020 `albumthumb` file paths work differently.  You must specify the path relative to the assets directory.  So - where before the `fish/_index.md` example content specified `fish_02.jpg` as the `albumthumb`, now it specifies `fish/fish_02.jpg`.  I apologize for the breaking change, but it really should've worked this way from the start.  It brings things in-line with the resources src, and the subalbum path specifications.

## Installation

Follow [Hugo's standard instructions](https://gohugo.io/getting-started/quick-start/#step-3-add-a-theme) for adding a theme to your site.

## Configuration

The exampleSite demonstrates the features unique to this theme.  In your site config params section the following extra parameters are supported:

* `favicon` - the favicon URL, relative to your site (placed in header meta tag)
* `description` - the description for the header meta tag
* `msvalidate` - MS validation tag
* `googlesiteverification` - Google site verification tag
* `thumb_width` - thumbnail width after resizing (default 480 pixels)
* `thumb_quality` - thumbnail encoding quality percentage after resizing (default 50%)
* `full_width` - display-sized image width after resizing (default 960 pixels)
* `full_quality` - display-sized image encoding quality after resizing (default 90%)

Additionally, `Author.name` and `Author.email` in the site config will display as the author and webmaster email.

## Album Construction

Inside your project create the directory `assets/NAME-OF-YOUR-ALBUM`.  Place all of one album's photos inside that directory.

Inside your project run:

```
$ hugo new NAME-OF-YOUR-ALBUM/_index.md
```

It will create an index file for your first album.  Open `content/NAME-OF-YOUR-ALBUM/_index.md` with your text editor. You'll see something like this:

```
---
title: "NAME-OF-YOUR-ALBUM"
date: "2020-03-15T00:00:00+00:00"
albumthumb: "NAME-OF-YOUR-ALBUM/photo00.jpg"
draft: false
resources:
- src: "NAME-OF-YOUR-ALBUM/photo00.jpg"
- src: "NAME-OF-YOUR-ALBUM/photo01.jpg"
- src: "NAME-OF-YOUR-ALBUM/photo02.jpg"
---
```

Change the title of your album if you wish, and set the filename of album's cover thumbnail.  The filename is relative to the assets folder, so if your album is named `dogs` and one of your images there is named `dog_01.jpg` you can put `dogs/dog_01.jpg` in `albumthumb` to select it.

In addition to those frontmatter options, you can also specify metadata for some or all of your images.  Do that by modifying the `resources` array with map elements.  The maps specify the image they apply to with the `src` key, as `src: "album/image.jpg"`.  You can then specify some or all of the following items: `alt`, `phototitle`, and `description`.  Demonstration of this is in the `exampleSite` directory albums.

### Sub-Albums

If you'd like to create an album that contains other albums - you can do that!  The way Autophugo handles this is by allowing you to create "groups" of albums.  The following command creates an album group called "dogs", for instance:

```
hugo new dogs/_index.md -k group
```

The resulting `content/dogs/_index.md` file looks like:

```
---
title: "Dogs"
date: 2020-03-15T14:00:00-06:00
albumthumb: "dogs/subalbum/photo_00.jpg"
type: "group"
---
```

The "group" is distinguished from a regular album from the `type` that's specified in there, and by the albums it contains...  Make sure to specify an albumthumb!

Now you would create albums inside that album group just like before...

```
hugo new dogs/pensive-dogs/_index.md
```

Your `assets` directory layout should mirror the directory layout in `content`.

See the `exampleSite` and the `dogs` folder and subfolders specifically.

### Note: About Subalbums

You can have subalbums in subalbums, just make sure to keep your `type`s straight.  The `exampleSite` has the `dogs` album group which two things in it: a `happy-dogs` album group, and a `pensive-dogs` subalbum.  The `happy-dogs` album group has two things in it: a `running-dogs` subalbum and a `stationary-dogs` subalbum.  Check out the way the `type` is specified in those groups and subalbums and compare it to what you're trying to do, if you're having trouble.

## Building the Site

Run `hugo` to build your site.  Output will be placed in the `public` directory.  The original images will not be included - only the resized versions.

When building your site, hugo must build thumbnails and distribution-sized images.  This process can take some time, especially if you have many pictures...  It stores versions of the images in the `resources` directory, so it doesn't have to redo the process every build.

Therefore - after adding an album your next build may take minutes.  Future ones will be quicker.

## Development Notes

If you try multiple sizes or quality settings for your images, you'll start to amass large numbers of images in your `resources` directory.  Once you settle on a quality and size you like you should consider deleting the resources and rebuilding to eliminate the unused images.

Regardless of the number of resources you have, Hugo will only deploy the ones actually used in a build.  Unused image resources will not be deployed.

## Comparison to Phugo

Unfortunately the [original Phugo](https://github.com/aerohub/phugo) hasn't been updated in a while, and was dropped from common theme lists.  AutoPhugo implements the pull requests over on Phugo, causing it to work error-free on modern Hugo.  Further, it sets standardized column layout (currently set at two, only), automatically builds albums based on files alone (Phugo required entering each filename as a shortcode), and automatically resizes photos for display and thumbnail.

## Acknowledgements

* Subgallery support - tfl0pz, Ognyan Nikolov
* [Magnific Popup lightbox](https://dimsemenov.com/plugins/magnific-popup/) - Dmitry Semenov

## License

The original template is released under the Creative Commons Attribution 3.0 License. Please keep the original attribution link when using for your own project.

The Magnific Popup lightbox is available under the MIT license, more info at their website linked above.
