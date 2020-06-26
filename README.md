# nalu-chunker

A transform stream which chunks incoming AVC/H264 bitstream into NAL unit chunks.

## API

```
const fs = require('fs');
const { H264Decoder } = require('h264decoder');
const NaluChunker = require('@eyevinn/nalu-chunker);

const naluChunker = new NaluChunker();
const decoder = new H264Decoder();

naluChunker.on('nalu', nalu => {
  console.log(`Got NAL unit ${nalu.type}`);
  const ret = decoder.decode(nalu.data);
  if (ret === H264Decoder.PIC_RDY) {
    console.log(`Got frame ${decoder.width}x${decoder.height}`);
    // decoder.pic contains YUV420p
  }
});

fs.createReadStream('file.h264')
  .pipe(naluChunker)
```

## License

MIT