 return (
    <RNImageBackground bgImage={bgImage} className={'flex-1 bg-secondaryColor'}>
     <KeyboardAvoidingView behavior={ios ? 'padding' : 'height'} className="flex-1">
     <RNView className={'flex-1'}>
        {device && (
          <ReanimatedCamera
          isActive={isActive}
          device={device}
          ref={cameraRef}
          videoStabilizationMode="auto"
          className="flex-1"
          format={format}
        />
        )}
      </RNView>
      <RNView className="absolute top-[10%] w-full justify-center items-center">
        <RNTextInput
          placeholder={'Donner un titre à votre live'}
          className={
            `bg-secondaryColor h-10 w-2/4 text-primaryText rounded-full text-center ${isTitle ? 'border-2 border-red-500' : ''}`
          }
          onChangeText={text => setRoomDetails({...roomDetails, title: text as string})}
          placeholderTextColor="#e0e0e0"
          value={roomDetails.title}
          onBlur={handleBlur}
        />
        {
          isTitle && (
            <RNText className="text-red-500 text-xs text-center">Le titre est obligatoire</RNText>
          )
        }
        {
          liveImage ? (
            <RNImageWithUri
              imageUrl={liveImage}
              className={'w-32 h-28 rounded-xl mt-8'}
              resizeMode="contain"
            />
          ) : (
            <RNPressable onPress={handlePickImage} className=" mt-8 justify-center bg-secondaryColor items-center rounded-lg">
          {/* <RNText className={'text-primaryText text-base'}>Ajouter une image de couverture</RNText> */}
          <RNImageWithLocal
            imageUrl={unionIcon}
            className={'w-36 h-36'}
          />
        </RNPressable>
          )
        }
          <RNPressable
            onPress={() => bottomSheetRefProducts.current?.open()}
            className="items-center mt-4 p-3 rounded-lg">
            <RNImageWithLocal
              imageUrl={commercialLive}
              className={'w-20 h-20 mt-1'}
              resizeMode="contain"
              tintColor={colors.text}
            />
          </RNPressable>
           {
            roomDetails.articles.length  > 0 && (
              <RNView className=" flex-row items-center">
                  {roomDetails.articles.map((item: any, index: number) => (
                    <ProductCardPicker
                      key={index}
                      item={item}
                      roomArticles={roomDetails}
                    />
                  ))}
                </RNView>
            )
           }
      </RNView>
      <RNView className=" absolute bottom-0 self-center">
        <RNPressableWithOpacity onPress={()=>{
          handleSaveLive(uid);
          }} className=" bg-primaryColor rounded-full items-center justify-center w-[209px] h-[60px] self-center mb-3">
          <RNText className=" text-backgroundColor text-xl font-pmedium text-center">
            Lancer le live
          </RNText>
        </RNPressableWithOpacity>
        </RNView>
      </KeyboardAvoidingView>
        <RNBottomSheet
         bottomSheetRef={bottomSheetRefProducts}
         height="75%"
         animationType="slide"
         style={{backgroundColor: colors.background}}
         >
          <RNScrollView
              contentContainerStyle={{ flexGrow: 1 }}
              showsVerticalScrollIndicator={false}
            >
          <PickerProductLive
            roomArticles={roomDetails}
            sellerProducts={sellerProducts}
            setRoomArticles={setRoomDetails}
            setSelectItem={setSelectItem}
            bottomSheetRefProducts={bottomSheetRefProducts}
          /></RNScrollView>
         </RNBottomSheet>
    </RNImageBackground>
  );   voici le return de la Screen pour creer un live
