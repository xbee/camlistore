# Search UI

The User Interface's "Search" box accepts predicates of the form
"[-]operator:value[:value]".  These predicates may be separated by 'and' or 'or'
keywords, or spaces which mean the same as 'and'. Expressions like this may be
grouped with parenthesis. Grouped expressions are evaluated first. Grouped
expressions may be negated.

An 'and' besides an 'or' is evaluated first. This means for example that

    tag:foo or is:pano tag:bar

will return all images having tag foo together with the panorama images having
tag bar.

Negation of a predicate is achieved by prepending a minus sign: -is:landscape
will match with pictures of not landscape ratio. For example:

    -(after:"2010-01-01" before:"2010-03-02T12:33:44") or loc:"Amsterdam"

will return all images having "modtime" outside the specified period, joined
with all images taken in Amsterdam.

When you need to match a value containing a space, you need to use double quotes
around the value only. For example: tag:"Three word tagname" and not "tag:Three
word tagname".  If your value contains double quotes you can use backslash
escaping.  For example:

    attr:bar:"He said: \"Hi\""

## Usable operators

**after**
: date format is RFC3339, but can be shortened as required.

**before**
: i.e. 2011-01-01 is Jan 1 of year 2011 and "2011" means the same.

**attr**
: match on attribute. Use attr:foo:bar to match nodes having their foo attribute
  set to bar, or attr:foo:~bar to match nodes whose foo attribute contains bar
  (case insensitive substring match).

**format**
: file's format (or MIME-type) such as jpg, pdf, tiff.

**has:location**
: image has a location (GPSLatitude and GPSLongitude can be retrieved from the
  image's EXIF tags).

**loc**
: uses the available metadata, such as EXIF GPS fields, or check-in locations,
  to match nodes having a location near the specified location.  Locations are
  resolved using maps.googleapis.com. For example: loc:"new york, new york"

**locrect**
: uses the various location metadata fields (such as EXIF GPS) to match nodes
  having a location within the specified location area. The area is defined by
  its North-West corner, followed and comma-separated by its South-East corner.
  Each corner is defined by its latitude, followed and comma-separated by its
  longitude. For example: locrect:48.63,-123.37,46.59,-121.28

**is:image**
: object is an image

**is:landscape**
: the image has a landscape aspect

**is:pano**
: the image's aspect ratio is over 2 - panorama picture.

**is:portrait**
: the image has a portrait aspect.

**height**
: use height:min-max to match images having a height of at least min and at most
  max. Use height:min- to specify only an underbound and height:-max to specify
  only an upperbound.  Exact matches should use height:480

**tag**
: match on a tag

**width**
: use width:min-max to match images having a width of at least min and at most
  max. Use width:min- to specify only an underbound and width:-max to specify
  only an upperbound.  Exact matches should use width:640

**filename**
: search for permanodes of files with this filename (case sensitive)

**childrenof**
: Find child permanodes of a parent permanode (or prefix of a parent permanode):
  childrenof:sha1-527cf12

**parentof**
: Find parent permanodes of a child permanode (or prefix of a child permanode):
  parentof:sha1-527cf12
