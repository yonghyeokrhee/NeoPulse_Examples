def createInputFile(filePath):
    ''' Creates a zip file with the required csv that is expected by the sagemaker.
    The zip file will contain a file called query.csv and the image file requested 
    by the user.

    Args:
        filePath (Path) - Path to the input image file.
    
    Returns:
        BytesIO - In memory zip file.

    '''
    
    # create the header to the file which is same as that used while training.
    queryHeaderContent = 'image\n'

    # create an inmemory file like object for the query csv
    queryFileObj = io.StringIO()
    queryFileObj.writelines(queryHeaderContent)

    # extract the input file name from the file path 
    inputFileName = filePath

    # Add the file name which relative query file.
    queryFileObj.writelines(inputFileName)
    # logger.info('Successfully constructed the input query file requeried for querying the model.')

    # Reading the input image into a byte array.
    imageFileBuffer=b''
    with open(str(filePath), "rb") as image:
        imageFileBuffer = bytearray(image.read())

    # Create the zip file

    inputZipFileObj = io.BytesIO()
    with ZipFile(inputZipFileObj, 'a', ZIP_DEFLATED, False) as zip:
        zip.writestr('query.csv', queryFileObj.getvalue())
        zip.writestr(inputFileName, imageFileBuffer)

    with open("input.zip", "wb") as f: # use `wb` mode
        f.write(inputZipFileObj.getvalue())

    return inputZipFileObj
    
    
if __name__ == '__main__':
  createInputFile('20200429_105534_005.jpg')
