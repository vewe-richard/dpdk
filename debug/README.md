# 1. simple l2fwd
Copy Makefile to app/test-pmd/Makefile to build l2fwd

```
diff debug/simple-l2fwd/app/test-pmd/Makefile app/test-pmd/Makefile
```

l2fwd-simple.c is a simple example which forwads packets between vlan 110 and vlan 120

### How to build?
Reference libmoon/build.sh
Without config file,
```
make config T=x86_64-native-linux-gcc O=x86_64-native-linux-gcc
sed -ri 's,(CONFIG_RTE_LIBRTE_IEEE1588=).*,\1y,' x86_64-native-linux-gcc/.config
if ${MLX5} ; then
	sed -ri 's,(MLX5_PMD=).*,\1y,' x86_64-native-linux-gcc/.config
fi
if ${MLX4} ; then
	sed -ri 's,(MLX4_PMD=).*,\1y,' x86_64-native-linux-gcc/.config
fi
```

After with presence of .config file
```
EXTRA_CFLAGS="-Wno-error" make -j $NUM_CPUS O=x86_64-native-linux-gcc
```

How to build for gdb?
```
EXTRA_CFLAGS="-Wno-error -g -O2" make -j $NUM_CPUS O=x86_64-native-linux-gcc
```

How to speed up compiling?
Update GNUMakefile in current directory with only app in directory list
