<style src="./annotationLayer.css"></style>
<script>
	import PdfjsWorker from 'pdfjs-dist/legacy/build/pdf.worker.js'
	import componentFactory from './componentFactory.js'

	if ( process.env.VUE_ENV !== 'server' ) {

		var pdfjsWrapper = require('./pdfjsWrapper.js').default;
		var PDFJS = require('pdfjs-dist/legacy/build/pdf.js');

		if ( typeof window !== 'undefined' && 'Worker' in window && navigator.appVersion.indexOf('MSIE 10') === -1 ) {

			// var PdfjsWorker = require('worker-loader!pdfjs-dist/legacy/build/pdf.worker.js');
			PDFJS.GlobalWorkerOptions.workerPort = new PdfjsWorker();
		}

		var component = componentFactory(pdfjsWrapper(PDFJS));
	} else {

		var component = componentFactory({});
	}

	export default component;
</script>