.PHONY: xos
xos: nodes.yaml images.yaml
	sudo docker-compose up -d
	../common/wait_for_xos_port.sh 80
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/setup.yaml
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/nodes.yaml
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/images.yaml

vtn: vtn_network_cfg_json
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/vtn-external.yaml

cord: virtualbng_json
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/mgmt-net.yaml
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /opt/xos/configurations/common/fixtures.yaml
	sudo docker-compose run xos python /opt/xos/tosca/run.py padmin@vicci.org /root/setup/cord-vtn-vsg.yaml

nodes.yaml:
	export SETUPDIR=.; bash ../common/make-nodes-yaml.sh

images.yaml:
	export SETUPDIR=.; bash ../common/make-images-yaml.sh

virtualbng_json:
	export SETUPDIR=.; bash ./make-virtualbng-json.sh

vtn_network_cfg_json:
	export SETUPDIR=.; bash ./make-vtn-networkconfig-json.sh

.PHONY: local_containers
local_containers:
	cd ../../../containers/xos; make devel
	cd ../../../containers/synchronizer; make