sudo -u geekotest -i ./rsync.pl --host localhost --verbose --add-existing caasp_dvd

Replace: (api key / secret from webui)

    #$client = OpenQA::Client->new(key => $options{'key'}, secret => $options{'secret'}, api => $openqa_url->host);
    $client = OpenQA::Client->new(apikey => '61464679564ED8D2', apisecret => '45E1299F4A43A3C4', api => $openqa_url->host);

    caasp_dvd => {
        #path => "dist.suse.de::repos/SUSE:/SLE-15:/Update:/Products:/CASP40/images/iso/",
        path => "dist.suse.de::repos/SUSE:/SLE-12-SP3:/Update:/Products:/CASP30/images/iso/",

TRY:
/usr/share/openqa/script/client isos post ISO=SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso DISTRI=caasp VERSION=3.0 FLAVOR=DVD ARCH=x86_64 BUILD=0101