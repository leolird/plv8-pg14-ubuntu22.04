# plv8-pg14-ubuntu22.04
##
## note: this is for ubuntu22.04/postgresql-14 !!!
##
# 1. unzip 
# 2. copy files to you pg14 path:  
sudo cp -r /your/path/of/plv8/extension/* /usr/share/postgresql/14/extension/
sudo cp -r /your/path/of/plv8/extension/*.so /usr/lib/postgresql/14/lib/
# 3. check:
CREATE EXTENSION plv8;

CREATE OR REPLACE FUNCTION plv8_test(keys text[], vals text[])
RETURNS text AS $$
var o = {};
for(var i=0; i<keys.length; i++){
o[keys[i]] = vals[i];
}
return JSON.stringify(o);
$$ LANGUAGE plv8 IMMUTABLE STRICT;

SELECT plv8_test(ARRAY['name', 'age'], ARRAY['Tom', '29']);

# the result should be like this:
---------------------------
{"name":"Tom","age":"29"}
