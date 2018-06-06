FROM ubuntu:18.04
MAINTAINER François Godin <copelnug@gmail.com>
CMD bash
		
RUN apt-get update && apt-get install -y libc6-dev
RUN apt-get update && apt-get install -y binutils

COPY --from=custom_gcc:latest /usr/local/lib64/libgcc_s.so.1 /usr/local/lib64/libgcc_s.so.1
COPY --from=custom_gcc:latest /usr/local/lib64/libgcc_s.so /usr/local/lib64/libgcc_s.so
COPY --from=custom_gcc:latest /usr/local/lib64/libstdc++.so.6.0.25 /usr/local/lib64/libstdc++.so.6.0.25
RUN ln -s /usr/local/lib64/libstdc++.so.6.0.25 /usr/local/lib64/libstdc++.so.6 && \
	ln -s /usr/local/lib64/libstdc++.so.6.0.25 /usr/local/lib64/libstdc++.so
COPY --from=custom_gcc:latest /usr/local/lib64/libstdc++.so.6.0.25-gdb.py /usr/local/lib64/libstdc++.so.6.0.25-gdb.py
COPY --from=custom_gcc:latest /usr/local/bin/gcc /usr/local/bin/gcc
COPY --from=custom_gcc:latest /usr/local/bin/g++ /usr/local/bin/g++
COPY --from=custom_gcc:latest /usr/local/include/c++/8.1.0 /usr/local/include/c++/8.1.0
COPY --from=custom_gcc:latest /usr/local/libexec/gcc/x86_64-linux-gnu/8.1.0 /usr/local/libexec/gcc/x86_64-linux-gnu/8.1.0
COPY --from=custom_gcc:latest /usr/local/lib/gcc/x86_64-linux-gnu/8.1.0/ /usr/local/lib/gcc/x86_64-linux-gnu/8.1.0/

# gcc installs .so files in /usr/local/lib64...
RUN set -ex; \
	echo '/usr/local/lib64' > /etc/ld.so.conf.d/local-lib64.conf; \
	ldconfig -v
