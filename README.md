# Leaflet.Export
Additional methods to L.map class provides export and print maps

## API
The following methods are added to the class:
  * export(exportOptions) - create a map canvas or image in a specified format;
  * exportDownload(downloadOptions) - save map image to specified file;
  * exportPrint(printOptions) - print map image;
  * supportedCanvasMimeTypes() - generates a list of supported data browser images formats for canvas.

### export(exportOptions)
Method export  create a map canvas or image in a specified format.
Returned value - promise.

The conversion process consists of two stages (steps in promise chain):
  * rendering maps canvas;
  * export canvas to the specified format.

Options:
  * format:
    * canvas - return canvas, contained rendered map;
  * image/png, image/jpeg, image/jpg, image/gif, image/bmp, image/tiff, image/x-icon, image/svg+xml, image/webp - return image in specified mime format. Developer can obtain list of the supported format  by using the method supportedCanvasMimeTypes().
  * caption:
    * text - header content (e.g. 'Map of Perm')
    * font - font description (e.g. '30px Arial')
    * fillStype - filled color (e.g. 'blue')
    * position - position in pixels of upper left corner of header (e.g.'10,100).
  * exclude - list of items are not displayed on the map when exporting;
  * afterRender - function to be called after rendering map;
  * afterExport - function to be called after export map.

If developer specify a custom function afterRender() after the rendering stage it receive shaped canvas. The function may be additional processing the canvas or perform other actions before second stage (export canvas to image).
Common template for afterRender is:

    afterRender(canvas) {
      operators...;
      return canvas;
    }

Function afterExport is called after export canvas to image.
Common template for afterRender is:

    afterRender(dataURL) {
      operators...;
      return dataURL;
    }

Exclude list can contain in any order next values:
  * excluded DOM-element;
  * text selector for excluded elements in DOM-format: .selectedClassOfDomElements, #elementId;
  * text selector for excluded elements in JQuery format: $(selector).
  (If JQuery is not supported an exception is generated.)

### exportDownload(downloadOptions)
Method exportDownload() calls the method export() to form the map image and stores the image in the specified file.
In addition to the options of the method export() method exportDownload()supports option fileName.
Use afterRender() and afterExport() functions developer can intercept control after this stages and perform additional actions.

### exportPrint(printOptions)
Method exportDownload() calls the method export() to form the map image prints the image.
Methods options consistent with the method of export options ()
Use afterRender() and afterExport() functions developer can intercept control after this stages and perform additional actions.
