<script>
	const checkImage = $event => {		
		let file = $event.currentTarget.files[0];
		loadImage.parseMetaData(file, function(data) {
		let orientation = 0;
		if (data.exif)
			orientation = data.exif.get('Orientation');		
		
		loadImage(file, function($canvas) {
				let base64data = $canvas.toDataURL('image/jpeg'),
				img_src = base64data.replace(/^data\:image\/\w+\;base64\,/, '');
				document.querySelector('.preview').src = base64data;			
			}, { orientation: orientation, canvas: true });
		});
	}
</script>

<img class="preview" src="" alt="Image Preview"><br>
<input type="file" on:change={ checkImage }>