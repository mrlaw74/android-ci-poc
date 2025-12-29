FROM ubuntu:22.04

ENV ANDROID_HOME=/opt/android-sdk
ENV ANDROID_SDK_ROOT=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools:$ANDROID_HOME/cmdline-tools/latest/bin

RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    wget unzip curl libglu1-mesa

RUN mkdir -p $ANDROID_HOME/cmdline-tools

# Download cmdline-tools
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O /tmp/cmdline-tools.zip \
    && unzip /tmp/cmdline-tools.zip -d /tmp \
    && mv /tmp/cmdline-tools $ANDROID_HOME/cmdline-tools/latest \
    && rm -rf /tmp/cmdline-tools.zip

# Accept licenses
RUN yes | sdkmanager --licenses

# Install packages
RUN sdkmanager \
    "platform-tools" \
    "platforms;android-33" \
    "emulator" \
    "system-images;android-33;google_apis;x86_64"

# Create AVD
RUN echo "no" | avdmanager create avd \
    -n test_avd \
    -k "system-images;android-33;google_apis;x86_64"

CMD emulator -avd test_avd -no-window -no-audio -gpu swiftshader_indirect
