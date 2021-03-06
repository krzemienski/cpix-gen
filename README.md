# cpix-gen
CPIX generator tool - dockerised

## install

```bash
docker pull unifiedstreaming/cpix-gen
```

## help

```bash
docker run unifiedstreaming/cpix-gen -h
```

## output to stdout

```bash
docker run unifiedstreaming/cpix-gen \
    --key 0D6B40238DA15E75AF6875C514C59B63:582D6B71611BE04C88E22AAA10441E2C \
    --usage_rule_preset 0D6B40238DA15E75AF6875C514C59B63 audio \
    --key E82F184C3AAA57B4ACE8606B5E3FEBAD:C2FAF66E2852CC4C4A751F0A2A941FDB \
    --usage_rule E82F184C3AAA57B4ACE8606B5E3FEBAD video:min_pixels=0,video:max_pixels=442368,bitrate:max_bitrate=500000 \
    --key 087BCFC6F7A55716B8406AA6EBA3369E:8281CE8DB9083697D9770D87DB962835 \
    --usage_rule_preset 087BCFC6F7A55716B8406AA6EBA3369E video_hd \
    --widevine \
    --playready \
    --playready.la_url https://test.playready.microsoft.com/service/rightsmanager.asmx \
    --stdout
```

produces

```xml
<?xml version='1.0' encoding='UTF-8'?>
<CPIX xmlns:pskc="urn:ietf:params:xml:ns:keyprov:pskc" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="urn:dashif:org:cpix" xsi:schemaLocation="urn:dashif:org:cpix cpix.xsd">
  <ContentKeyList>
    <ContentKey kid="0d6b4023-8da1-5e75-af68-75c514c59b63">
      <Data>
        <pskc:Secret>
          <pskc:PlainValue>WC1rcWEb4EyI4iqqEEQeLA==</pskc:PlainValue>
        </pskc:Secret>
      </Data>
    </ContentKey>
    <ContentKey kid="e82f184c-3aaa-57b4-ace8-606b5e3febad">
      <Data>
        <pskc:Secret>
          <pskc:PlainValue>wvr2bihSzExKdR8KKpQf2w==</pskc:PlainValue>
        </pskc:Secret>
      </Data>
    </ContentKey>
    <ContentKey kid="087bcfc6-f7a5-5716-b840-6aa6eba3369e">
      <Data>
        <pskc:Secret>
          <pskc:PlainValue>goHOjbkINpfZdw2H25YoNQ==</pskc:PlainValue>
        </pskc:Secret>
      </Data>
    </ContentKey>
  </ContentKeyList>
  <DRMSystemList>
    <DRMSystem kid="0d6b4023-8da1-5e75-af68-75c514c59b63" systemId="edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
      <PSSH>AAAAinBzc2gBAAAA7e+LqXnWSs6jyCfc1R0h7QAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAA2EhANa0AjjaFeda9odcUUxZtjEhDoLxhMOqpXtKzoYGteP+utEhAIe8/G96VXFrhAaqbrozae</PSSH>
    </DRMSystem>
    <DRMSystem kid="e82f184c-3aaa-57b4-ace8-606b5e3febad" systemId="edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
      <PSSH>AAAAinBzc2gBAAAA7e+LqXnWSs6jyCfc1R0h7QAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAA2EhANa0AjjaFeda9odcUUxZtjEhDoLxhMOqpXtKzoYGteP+utEhAIe8/G96VXFrhAaqbrozae</PSSH>
    </DRMSystem>
    <DRMSystem kid="087bcfc6-f7a5-5716-b840-6aa6eba3369e" systemId="edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
      <PSSH>AAAAinBzc2gBAAAA7e+LqXnWSs6jyCfc1R0h7QAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAA2EhANa0AjjaFeda9odcUUxZtjEhDoLxhMOqpXtKzoYGteP+utEhAIe8/G96VXFrhAaqbrozae</PSSH>
    </DRMSystem>
    <DRMSystem kid="0d6b4023-8da1-5e75-af68-75c514c59b63" systemId="9a04f079-9840-4286-ab92-e65be0885f95">
      <PSSH>AAAELnBzc2gBAAAAmgTweZhAQoarkuZb4IhflQAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAPa2gMAAAEAAQDQAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADIALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAFMAPgA8AEsASQBEACAAQQBMAEcASQBEAD0AIgBBAEUAUwBDAFQAUgAiACAAQwBIAEUAQwBLAFMAVQBNAD0AIgBPAEUAdQBNAHkARABlAFEAMQBzADgAPQAiACAAVgBBAEwAVQBFAD0AIgBJADAAQgByAEQAYQBHAE4AZABWADYAdgBhAEgAWABGAEYATQBXAGIAWQB3AD0APQAiAD4APAAvAEsASQBEAD4APABLAEkARAAgAEEATABHAEkARAA9ACIAQQBFAFMAQwBUAFIAIgAgAEMASABFAEMASwBTAFUATQA9ACIAKwBOAFYAOQAvADgAagBiAGYAcgB3AD0AIgAgAFYAQQBMAFUARQA9ACIAVABCAGcAdgA2AEsAbwA2AHQARgBlAHMANgBHAEIAcgBYAGoALwByAHIAUQA9AD0AIgA+ADwALwBLAEkARAA+ADwASwBJAEQAIABBAEwARwBJAEQAPQAiAEEARQBTAEMAVABSACIAIABDAEgARQBDAEsAUwBVAE0APQAiAFoAMQAwAGkATwBZAFkAegBIADMAawA9ACIAIABWAEEATABVAEUAPQAiAHgAcwA5ADcAQwBLAFgAMwBGAGwAZQA0AFEARwBxAG0ANgA2AE0AMgBuAGcAPQA9ACIAPgA8AC8ASwBJAEQAPgA8AC8ASwBJAEQAUwA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEwAQQBfAFUAUgBMAD4AaAB0AHQAcABzADoALwAvAHQAZQBzAHQALgBwAGwAYQB5AHIAZQBhAGQAeQAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBzAGUAcgB2AGkAYwBlAC8AcgBpAGcAaAB0AHMAbQBhAG4AYQBnAGUAcgAuAGEAcwBtAHgAPAAvAEwAQQBfAFUAUgBMAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=</PSSH>
    </DRMSystem>
    <DRMSystem kid="e82f184c-3aaa-57b4-ace8-606b5e3febad" systemId="9a04f079-9840-4286-ab92-e65be0885f95">
      <PSSH>AAAELnBzc2gBAAAAmgTweZhAQoarkuZb4IhflQAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAPa2gMAAAEAAQDQAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADIALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAFMAPgA8AEsASQBEACAAQQBMAEcASQBEAD0AIgBBAEUAUwBDAFQAUgAiACAAQwBIAEUAQwBLAFMAVQBNAD0AIgBPAEUAdQBNAHkARABlAFEAMQBzADgAPQAiACAAVgBBAEwAVQBFAD0AIgBJADAAQgByAEQAYQBHAE4AZABWADYAdgBhAEgAWABGAEYATQBXAGIAWQB3AD0APQAiAD4APAAvAEsASQBEAD4APABLAEkARAAgAEEATABHAEkARAA9ACIAQQBFAFMAQwBUAFIAIgAgAEMASABFAEMASwBTAFUATQA9ACIAKwBOAFYAOQAvADgAagBiAGYAcgB3AD0AIgAgAFYAQQBMAFUARQA9ACIAVABCAGcAdgA2AEsAbwA2AHQARgBlAHMANgBHAEIAcgBYAGoALwByAHIAUQA9AD0AIgA+ADwALwBLAEkARAA+ADwASwBJAEQAIABBAEwARwBJAEQAPQAiAEEARQBTAEMAVABSACIAIABDAEgARQBDAEsAUwBVAE0APQAiAFoAMQAwAGkATwBZAFkAegBIADMAawA9ACIAIABWAEEATABVAEUAPQAiAHgAcwA5ADcAQwBLAFgAMwBGAGwAZQA0AFEARwBxAG0ANgA2AE0AMgBuAGcAPQA9ACIAPgA8AC8ASwBJAEQAPgA8AC8ASwBJAEQAUwA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEwAQQBfAFUAUgBMAD4AaAB0AHQAcABzADoALwAvAHQAZQBzAHQALgBwAGwAYQB5AHIAZQBhAGQAeQAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBzAGUAcgB2AGkAYwBlAC8AcgBpAGcAaAB0AHMAbQBhAG4AYQBnAGUAcgAuAGEAcwBtAHgAPAAvAEwAQQBfAFUAUgBMAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=</PSSH>
    </DRMSystem>
    <DRMSystem kid="087bcfc6-f7a5-5716-b840-6aa6eba3369e" systemId="9a04f079-9840-4286-ab92-e65be0885f95">
      <PSSH>AAAELnBzc2gBAAAAmgTweZhAQoarkuZb4IhflQAAAAMNa0AjjaFeda9odcUUxZtj6C8YTDqqV7Ss6GBrXj/rrQh7z8b3pVcWuEBqpuujNp4AAAPa2gMAAAEAAQDQAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADIALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAFMAPgA8AEsASQBEACAAQQBMAEcASQBEAD0AIgBBAEUAUwBDAFQAUgAiACAAQwBIAEUAQwBLAFMAVQBNAD0AIgBPAEUAdQBNAHkARABlAFEAMQBzADgAPQAiACAAVgBBAEwAVQBFAD0AIgBJADAAQgByAEQAYQBHAE4AZABWADYAdgBhAEgAWABGAEYATQBXAGIAWQB3AD0APQAiAD4APAAvAEsASQBEAD4APABLAEkARAAgAEEATABHAEkARAA9ACIAQQBFAFMAQwBUAFIAIgAgAEMASABFAEMASwBTAFUATQA9ACIAKwBOAFYAOQAvADgAagBiAGYAcgB3AD0AIgAgAFYAQQBMAFUARQA9ACIAVABCAGcAdgA2AEsAbwA2AHQARgBlAHMANgBHAEIAcgBYAGoALwByAHIAUQA9AD0AIgA+ADwALwBLAEkARAA+ADwASwBJAEQAIABBAEwARwBJAEQAPQAiAEEARQBTAEMAVABSACIAIABDAEgARQBDAEsAUwBVAE0APQAiAFoAMQAwAGkATwBZAFkAegBIADMAawA9ACIAIABWAEEATABVAEUAPQAiAHgAcwA5ADcAQwBLAFgAMwBGAGwAZQA0AFEARwBxAG0ANgA2AE0AMgBuAGcAPQA9ACIAPgA8AC8ASwBJAEQAPgA8AC8ASwBJAEQAUwA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEwAQQBfAFUAUgBMAD4AaAB0AHQAcABzADoALwAvAHQAZQBzAHQALgBwAGwAYQB5AHIAZQBhAGQAeQAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBzAGUAcgB2AGkAYwBlAC8AcgBpAGcAaAB0AHMAbQBhAG4AYQBnAGUAcgAuAGEAcwBtAHgAPAAvAEwAQQBfAFUAUgBMAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=</PSSH>
    </DRMSystem>
  </DRMSystemList>
  <ContentKeyUsageRuleList>
    <ContentKeyUsageRule kid="0d6b4023-8da1-5e75-af68-75c514c59b63">
      <AudioFilter/>
    </ContentKeyUsageRule>
    <ContentKeyUsageRule kid="087bcfc6-f7a5-5716-b840-6aa6eba3369e">
      <VideoFilter minPixels="442369" maxPixels="2073600"/>
    </ContentKeyUsageRule>
    <ContentKeyUsageRule kid="e82f184c-3aaa-57b4-ace8-606b5e3febad">
      <VideoFilter minPixels="0" maxPixels="442368"/>
      <BitrateFilter maxBitrate="500000"/>
    </ContentKeyUsageRule>
  </ContentKeyUsageRuleList>
</CPIX>
```



## output to file

```bash
docker run -v $PWD:/data unifiedstreaming/cpix-gen \
    --key 0D6B40238DA15E75AF6875C514C59B63:582D6B71611BE04C88E22AAA10441E2C \
    --usage_rule_preset 0D6B40238DA15E75AF6875C514C59B63 audio \
    --key E82F184C3AAA57B4ACE8606B5E3FEBAD:C2FAF66E2852CC4C4A751F0A2A941FDB \
    --usage_rule E82F184C3AAA57B4ACE8606B5E3FEBAD video:min_pixels=0,video:max_pixels=442368,bitrate:max_bitrate=500000 \
    --key 087BCFC6F7A55716B8406AA6EBA3369E:8281CE8DB9083697D9770D87DB962835 \
    --usage_rule_preset 087BCFC6F7A55716B8406AA6EBA3369E video_hd \
    --widevine \
    --playready \
    --playready.la_url https://test.playready.microsoft.com/service/rightsmanager.asmx \
    --output /data/example.cpix
```

produces the same as the previous example, but in the file `example.cpix`
