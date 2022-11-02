# locative
mapping the locations of immersive content

<p>This is a demo of adding locative video to a webmap. From going out on a trail with a gopro to putting that content into a web map where clicking on a location will give the video content at that location</p>

<h3>Recipe</h3>
<p>To use this repo, several steps are required in collecting and processing data before it can be displayed on a map. Briefly, these steps are listed here</p>

<ol>
    <li>First, use a video capture device capable of recording video with GPS metadata such as a GoPro or Insta360 Camera. Ensure that location recording is enabled, and that the dvice has a GPS fix before starting the recording. After capturing, you have have to enable GPS metadata output using the pre-processing software for your device. Using the GoPro MAX for example, you will need to use GoPro Player and ensure that GPMF data is included in the HEVC Mp4 video output.</li>
    <li>Using a software such as <a href='https://exiftool.org'>EXIF Tool</a> Extract the gps location data embedded in the video file as a GPX file. In the utils of this repo I've included the GPX.fmt file that will ensure the correct GPX format is created. The important element to extract is <b>Time</b> as this allows for the keying of location to video. If you are using more than one video file, make sure you extract each GPX for each video.</li>
    <li>Upload the video files to Youtube and set visibility to Public or Unlisted (<i>not private</i>). Copy the sharable link(s) to where you can find them.</li>
    <li>Currently, keying between the video file and the location is through the attribute table of the GPX file. each GPX track point needs a time delta from the beginning of the video. This is calculated by taking the time of the first GPX point (when the video starts) and subtracting it from the current GPS point, in seconds. You can store this time delta in a attribute field, or carrying the calculation into hte next step </li> 
    <li>Each GPX file will have a correlating Youtube sharing link. Add a field to the GPX file called videotime. For each row in the GPX table (the track points), setthe videotime field to be the youtube embed link <i>plus</i> ?start= and the time delta value made earlier. this will look something like www.youtube.com/embed/EHDHSCNFHS?start=123 (where EHDHSCNFHS is the unique video identifier)</li>
    <li>Merge the GPX files into a single layer</li>
    <li>save the GPX file as a GeoJSON file type and upload to a free <a href='https://developers.arcgis.com/sign-in/'>ESRI developer account</a>. If you haven't created one yet, its pretty easy. At the same time, note your API key as you will need it</li>
    <li>replace the esri api key in the index.html with the one in your esri devloper account. </li>
    <li>for the GeoJSON file upaloded to esri's developer account, grab its 'point layer url' forthe Feature Layer version of the file. Use this as the url field in the Feature Layer of the index.html javascript. </li>
</ol>

<p> as you can see, this script is very much in beta, and will become more streamlined in time. In particular, the preprocessing steps for the attribute table can be significantly automated.</p>